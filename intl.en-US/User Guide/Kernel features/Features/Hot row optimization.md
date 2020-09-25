# Hot row optimization

This topic describes how to use the hot row optimization feature to improve the performance of database systems.

## Prerequisites

The PolarDB cluster version is PolarDB for MySQL 5.6 and the minor kernel version is 20200616 or later.

**Note:** For more information about how to upgrade the minor kernel version, see [Upgrade the revision version](/intl.en-US/User Guide/Kernel features/Upgrade the revision version.md).

## Limits

The hot row optimization feature is not applicable in the following scenarios:

-   Hot rows are stored in a partitioned table.
-   The table that stores hot rows is associated with a trigger.

## Considerations

PolarDB for MySQL uses canary releases to provide the hot row optimization feature. To use this feature, [Submit a ticket](https://workorder-intl.console.aliyun.com/)for technical support.

## Background information

In database systems, data in some rows are added, deleted, modified, and queried at a high frequency. These data rows are called hot rows. When a transaction updates data in a row, the transaction must hold the row lock before the transaction is committed or rolled back. Transactions cannot update data in the same row at the same time. Therefore, the other transactions must wait for the transaction to release the row lock. Requests to update a single hot row are processed in serial. Therefore, traditional sharding policies are ineffective in improving database performance.

In e-commerce platforms, limited sales and flash sales are frequently used for promotion. In these promotion scenarios, a large number of requests to update a single hot row are sent to the backend database system in a short period. This results in row lock contention and queues for acquiring row locks. This degrades the system performance. If an update request waits for a long time before the update request is processed, services are affected in a significant way.

In this case, you cannot achieve the expected low latency by improving your hardware configurations. To resolve this issue, PolarDB provides an innovative method to optimize the kernel layer of the database. The optimized kernel layer can automatically identify the requests to update hot rows, and divide the requests to update the same hot row within the specified period into groups. Different groups of the requests are processed in parallel in pipelines. This improves system performance in a significant way.

## Optimizations

-   From serial processing to parallel processing in pipelines

    Parallel processing is the easiest way to improve the performance of database systems. However, the system needs to handle considerable challenges to process the requests of updating the same hot row in parallel. PolarDB uses pipelines to process the update requests in an innovative way. This maximizes the capabilities to process the requests of updating the same hot row in parallel.

    ![1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2632729951/p133270.png)

    The SQL statements that are executed to update hot rows are attached with the autocommit or commit\_on\_success label. The optimized MySQL kernel layer can automatically identify update requests that are attached with the autocommit or commit\_on\_success label. The kernel layer can also implement hashing on the collected update requests based on primary keys or unique keys. After hashing, the update requests that are allocated to the same bucket are processed and committed in groups and batches based on the time of arriving at the bucket.

    To allow these update requests to be processed in pipelines, two execution units are required to divide the update requests into two groups. When the update requests in the first group are collected and are ready to commit, the update requests in the second group start to be collected. When the update requests in the second group are collected and are ready to commit, the update requests in the first group have been committed. The next batch of the update requests start to be collected in the first group, and so on. This ensures that the update requests can be processed in parallel.

    Multi-core CPUs are widely used. This pipelined processing method can make full use of hardware resources, optimize CPU usage, and improve the parallel processing capability of database systems. This maximizes the throughput of the database systems.

-   Eliminate the need to wait for acquiring row locks

    A data row must be locked when the data row is updated. This ensures the logical consistency of data. If the requests of acquiring row locks are not processed immediately and wait in a queue, the request processing latency is increased and deadlock detection is triggered. This consumes additional resources.

    The requests to update the same data row are grouped in chronological order. The first update request in a group serves as a leader. The leader reads data in the data row and locks the data row. The other update requests in the same group serve as followers. If the data row is locked by the leader, the followers can acquire the row locks immediately.

    This optimization method reduces the times for acquiring row locks and saves time. This improves the performance of the entire database system.

-   Reduce the traversals of B-tree indexes

    MySQL manages data based on B-tree indexes. During each query, MySQL traverses all the indexes to locate the required data row. The traversal requires a long time if the table is large and has many index levels.

    If the grouping mechanism is used, only the leader of each group needs to traverse the indexes to locate the required data row. Then, the leader caches the updated data row to the memory. The followers in the same group can read the data row from the memory after they acquire the row lock, and do not need to traverse the indexes again.

    This reduces the number of index traversals and saves time.


## Use the hot row optimization feature

-   Before you use the hot row optimization feature to improve the performance of database systems, you must specify the parameters that are described in the following table.

    |Parameter|Description|
    |---------|-----------|
    |hotspot|Specifies whether to enable the hot row optimization feature. Valid values: ON and OFF. Default value: OFF.|
    |hotspot\_for\_autocommit|Specifies whether to enable the hot row optimization feature to optimize the UPDATE statement that is in the auto-commit mode. Valid values: ON and OFF. Default value: OFF.**Note:** You can specify this parameter only when the hotspot parameter is set to ON. |
    |hotspot\_update\_max\_wait\_time|The time during which the leader in a group waits for the followers to join the group in the process of updating row data in groups and batches. Unit: microseconds. Default value: 100 μs.|
    |hotspot\_lock\_type|Specifies whether to use a new type of row locks in the process of updating row data in groups and batches. Valid values: ON and OFF. Default value: OFF.**Note:** If this parameter is set to ON, the requests to update the same hot row do not need to wait for acquiring row locks. This improves the performance of database systems. |

    **Note:**

    -   To use the hot row optimization feature, you must enable the binary logging feature. Therefore, if you set the hotspot parameter to ON when the binary logging feature is disabled, an error is reported.

        The following error message appears.

        ```
        MySQL [(none)]> set global hotspot=ON;
        ERROR 3042 (HY000):
        Variable 'hotspot' cannot be enabled because 'bin logging' is enabled/disabled
        ```

    -   When binary logging is globally enabled but disabled for sessions, you can set the hotspot parameter to ON. However, hot row optimization does not take effect on the UPDATE statement.
    -   If you set the hotspot parameter to ON after the rds\_ic\_reduce\_hint\_enable parameter is set to ON, the following error message appears.

        ```
        MySQL [(none)]> set global rds_ic_reduce_hint_enable=ON;
        MySQL [(none)]> set global hotspot=ON;
        ERROR 3042 (HY000): Variable 'hotspot' cannot be enabled because 'rds_ic_reduce_hint_enable' is enabled/disabled
        ```

-   You can execute the following statement to check the parameter settings:

    ```
    show variables like "hotspot%";
    ```

    Example

    ```
    MySQL [(none)]> show variables like "hotspot%";
    +------------------------------+-------+
    |
    Variable_name                | Value |
    +------------------------------+-------+
    |
    hotspot                      | OFF   |
    |
    hotspot_for_autocommit       | OFF   |
    |
    hotspot_lock_type            | OFF   |
    |
    hotspot_update_max_wait_time | 100   |
    +------------------------------+-------+
    ```

-   You can execute the following statement to view the statistics of hot row optimization:

    ```
    show global status like 'Group_update%';
    ```


## Performance testing

-   The following CREATE TABLE and UPDATE statements are executed for performance testing.
    -   CREATE TABLE statement

        ```
        CREATE TABLE sbtest(id INT UNSIGNED NOT NULL, c BIGINT UNSIGNED NOT NULL) PRIMARY KEY (id)
        ```

    -   UPDATE statement

        ```
        UPDATE COMMIT_ON_SUCCESS ROLLBACK_ON_FAIL QUEUE_ON_PK 1 TARGET_AFFECT_ROW 1 sbtest SET c=c+1 WHERE id = 1
        ```

-   SysBench is used to test the performance of database systems in the following scenarios:
    -   Scenario 1: One hot row and 8-core CPUs

        In this scenario, 8-core CPUs are used and a large number of concurrent requests are sent to update a single hot row. After hot row optimization is enabled, the performance of the database system is improved by approximately 64 times.

        ![2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2632729951/p133340.png)

    -   Scenario 2: One hot row and 32-core CPUs

        In this scenario, 32-core CPUs are used and concurrent requests are sent to update a single hot row. After hot row optimization is enabled, the maximum of queries per second \(QPS\) is improved by 63 times. When the number of concurrent requests reaches 8,000, the performance of the database system is improved by 45 times.

        ![2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3632729951/p133341.png)

    -   Scenario 3: Eight hot rows and 32-core CPUs

        In this scenario, 32-core CPUs are used and concurrent requests are sent to update eight hot rows. After hot row optimization is enabled, the maximum of QPS is improved by 20 times.

        When the number of concurrent requests reaches 16,000, database failures occur and no results are returned if hot row optimization is disabled. However, if hot row optimization is enabled, row data is updated as expected and QPS remains stable.

        ![4](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3632729951/p133342.png)


