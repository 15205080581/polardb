# Release notes of the PolarDB kernel

This topic describes the updates and features of the PolarDB for MySQLdatabase kernel.

The following figure shows the position of the PolarDB database engine in the PolarDB architecture.

![1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2307320061/p132915.png)

For more information about the architecture and features of PolarDB, see [Architecture](/intl.en-US/Product Introduction/Architecture.md).

## Features of the PolarDB database kernel

|Category|Feature|5.6|8.0|
|--------|-------|---|---|
|Online transaction processing \(OLTP\) performance|The hot row optimization feature is supported and is applicable to flash sales scenarios. For more information, see [Hot row optimization](/intl.en-US/User Guide/Kernel features/Features/Hot row optimization.md).|Supported. The version of the kernel must be 20200616 or later.|Not supported.|
|[Thread pools](/intl.en-US/User Guide/Kernel features/Features/Thread Pool.md) are supported.|Supported. The version of the kernel must be 20200423 or later.|Supported. The version of the kernel must be 8.0.1.1.1 or later.|
|Online analytical processing \(OLAP\) performance|[Parallel queries](/intl.en-US/User Guide/Kernel features/Parallel query/Parallel queries.md) are supported.|Not supported.|Supported. The version of the kernel must be 8.0.1.0.5 or later.|
|Semijoins are supported for parallel queries. For more information, see [Perform semijoins in parallel](/intl.en-US/User Guide/Kernel features/Parallel query/Perform semijoins in parallel.md).|Not supported.|Supported. The version of the kernel must be 8.0.1.1.2 or later.|
|The UNION operator is supported for parallel queries.|Not supported.|Supported. The version of the kernel must be 8.0.1.1.3 or later.|
|Hash joins are supported for parallel queries. For more information, see [Hash joins in parallel queries](/intl.en-US/User Guide/Kernel features/Parallel query/Hash joins in parallel queries.md).|Not supported.|Supported. The version of the kernel must be 8.0.2.1.0 or later.|
|Security|The recycle bin feature is supported. This prevents data loss that is caused by accidental DROP operations. For more information, see [Recycle bin](/intl.en-US/User Guide/Kernel features/Recycle Bin.md).|Not supported.|Supported. The version of the kernel must be 8.0.1.1.2 or later.|

## Query the kernel version

-   For PolarDB for MySQL 8.0, execute the following statements to query the kernel version:

    -   If your cluster is created after February 5, 2020, execute the following statement:

        ```
        show variables like "%polardb_version%";
        ```

    -   If your cluster is created on or before February 5, 2020, execute the following statement:

        ```
        show variables like '%rds_release_date%';
        ```

    To view the time when the cluster is created, log on to the [PolarDB console](https://polardb.console.aliyun.com/), find the cluster, and click the cluster ID. On the **Overview** page, you can view the value of the **Created At** parameter.

    ![Creation time](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2373320061/p161823.png)

-   For PolarDB for MySQL 5.6, execute the following statement to query the kernel version:

    ```
    show variables like '%rds_release_date%';
    ```


**Note:** For more information about the version of the PolarDB database kernel, see [Version of the PolarDB database kernel](/intl.en-US/User Guide/Kernel features/Version of the PolarDB database kernel.md).

## PolarDB for MySQL 8.0 release notes

The following table describes the versions and the features that are supported by PolarDB for MySQL 8.0.

|Minor version|Revision version|Release date|Minor MySQL version that is fully compatible with PolarDB for MySQL|Released feature|
|-------------|----------------|------------|-------------------------------------------------------------------|----------------|
|8.0.2.x|8.0.2.1.1|20200826|8.0.18|Several known bugs are fixed.|
|8.0.2.1.0|20200722|8.0.18|-   Hash joins are supported for parallel queries. For more information, see [Hash joins in parallel queries](/intl.en-US/User Guide/Kernel features/Parallel query/Hash joins in parallel queries.md).
-   The CPU usage of each SQL statement can be monitored in real time. The Performance Agent and warm buffer pool features are supported. For more information, see [Resource Manager](/intl.en-US/User Guide/Kernel features/Performance data monitoring/Resource Manager.md), and [Performance Agent](/intl.en-US/User Guide/Kernel features/Performance data monitoring/Performance Agent.md) . |
|8.0.1.x|8.0.1.1.4|20200704|8.0.13|-   Data definition language \(DDL\) statements can be executed in parallel to improve the execution efficiency of the DDL statements.
-   The length of each queue of the simulated asynchronous I/O \(AIO\) can be dynamically adjusted.
-   Data in a full-text search \(FTS\) index cache can be synchronized between the primary node and read-only nodes. This ensures cache coherence. |
|8.0.1.1.3|20200529|8.0.13|The parallel query feature is improved.|
|8.0.1.1.2|20200409|8.0.13|-   The recycle bin feature is supported. This prevents data loss that is caused by accidental DROP operations. For more information, see [Recycle bin](/intl.en-US/User Guide/Kernel features/Recycle Bin.md).
-   The operations that are performed on temporary tables compromises the performance. This version is optimized to reduce the negative impact of these operations on performance.
-   The parallel query feature is improved. |
|8.0.1.1.1|20200328|8.0.13|-   The thread pool feature is supported. For more information, see [Thread pool](/intl.en-US/User Guide/Kernel features/Features/Thread Pool.md).
-   Global database networks \(GDNs\) are supported. For more information, see [Global database networks](/intl.en-US/User Guide/Deployment Architecture/Global database networks/Create a GDN and a secondary cluster.md).
-   The parallel query feature is improved. |
|8.0.1.1.0|20200205|8.0.13|-   The cost model for parallel queries is improved.
-   The thread scheduling capabilities of parallel query executors are enhanced. |
|8.0.1.0.6|20200101|8.0.13|Several known bugs are fixed.|
|8.0.1.0.5|20191203|8.0.13|Diagnosis information about the execution plans of parallel queries is added. This makes the execution plans easy to read.|

-   8.0.2.1.1\(20200826\)

    |Category|Description|
    |--------|-----------|
    |Added features and performance optimization|The write performance of clusters is optimized.|
    |Bugs fixed|The memory leak bug is fixed.|

-   8.0.2.1.0\(20200722\)

    |Category|Description|
    |--------|-----------|
    |Added features and performance optimization|The EXPLAIN statement can be executed to query the execution plan of parallel queries. After you specify FORMAT=TREE in the EXPLAIN statement, the execution plan is displayed in the TREE format.|
    |Hash joins are supported for parallel queries. The performance of JOIN operations that do not use indexes is improved. For more information, see [Hash joins in parallel queries](/intl.en-US/User Guide/Kernel features/Parallel query/Hash joins in parallel queries.md).|
    |The Resource Manager feature is added to monitor CPU and memory resources. For more information, see [Resource Manager](/intl.en-US/User Guide/Kernel features/Performance data monitoring/Resource Manager.md).|
    |The Performance Agent feature is added to collect the statistics about the performance metrics of PolarDB for MySQL instances. To obtain the performance metric data, you can also query the data that is stored in the PERF\_STATISTICS in-memory table. For more information, see [Performance Agent](/intl.en-US/User Guide/Kernel features/Performance data monitoring/Performance Agent.md).|
    |The warm buffer pool feature is supported. When a PolarDB for MySQL instance restarts after a breakdown or is upgraded, data in the buffer pool remains available. This accelerates the restart process, and ensures that the performance is not compromised after the restart.|

-   8.0.1.1.4\(20200704\)

    |Category|Description|
    |--------|-----------|
    |Added features and performance optimization|DDL statements can be executed in parallel to improve the execution efficiency of the DDL statements.|
    |The length of each queue of the simulated AIO can be dynamically adjusted.|
    |Data in an FTS index cache can be synchronized between the primary node and read-only nodes. This ensures cache coherence.|
    |A WHERE clause supports subqueries that include aggregate functions. If the subqueries that include aggregate functions support index scans, the subqueries can be executed in parallel.|
    |In earlier versions, the operations of locking or unlocking instances take effect for only standard tables. In this version, the operations of locking or unlocking instances take effect for temporary tables and standard tables.|
    |Bugs fixed|The following bug is fixed: Instances become unavailable because some DDL statements are being replicated when the primary node serves as a read-only node.|
    |The following bug is fixed: The write throughput is decreased and the write latency is increased because thread pools are enabled.|
    |The following bug is fixed: Deadlocks occur because binary logs are purged.|
    |Memory leak bugs are fixed.|
    |Bugs that occur in high availability scenarios are fixed.|

-   8.0.1.1.3\(20200529\)

    |Category|Description|
    |--------|-----------|
    |Added features and performance optimization|Security is enhanced by improving password management and other security operations.|
    |The performance of parallel queries is enhanced in the following scenarios:    -   The GROUP BY, UNION, and SELECT COUNT\(\*\) FROM <table\> statements are executed.
    -   Shared InnoDB temporary tables are used for execution plans in parallel subqueries.
    -   The views, derived tables, and temporary tables are used in execution plans.
    -   Temporary tables can be used for parallel queries, but the following limits must be met:
        -   If you do not specify conditions in the SELECT COUNT\(\*\) statement to query data in temporary tables, parallel queries are not supported.
        -   Parallel queries are not supported for in-memory temporary tables. |
    |An audit log format is supported. If audit logs are collected in this format, the log file includes a field that contains virtual IP addresses.|
    |The rate of idle space to total space on index pages can be managed. This reduces latch contention and the probability of performing structure modification operations \(SMOs\), and improves write performance.|
    |Simulated AIO among multiple queues is supported. This improves dirty page flushing and write performance.|
    |Buffer pool pages can be excluded from core files. This reduces the sizes of the core files and minimizes the impact on online services.|
    |Bugs fixed|In earlier versions, if the upper memory limit for the TempTable storage engine is reached, the TempTable storage engine reports an out-of-memory error instead of moving data from memory to disks. This bug is fixed in this version.|
    |The following bug is fixed: Instances become unavailable when the sort buffer size is set to a small value and ORDER BY is used in InnoDB FTS.|
    |The following bug is fixed: If a temporary table contains duplicate column names, the requested fields fail to be returned.|
    |The following bug is fixed: In parallel queries, when the MAX or MIN function is used in conjunction with GROUP BY and a loose index scan is used, the statement is still being executed after the query is killed.|
    |Several bugs that are related to failovers are fixed.|
    |Several bugs that are related to parallel queries are fixed.|
    |The following bug is fixed: If you execute the SHOW BINARY LOGS statement, transactions may not be committed.|

-   8.0.1.1.2\(20200409\)

    |Category|Description|
    |--------|-----------|
    |Added features and performance optimization|The sorting method is optimized. Column values are first sorted based on string prefixes and then based on entire strings. To be more specific, if the string prefixes of the column values are the same, the column values are sorted based on the entire strings. For columns that contain the values of the CHAR and VARCHAR data types, you can specify the prefix length to accelerate the comparison process and reduce sorting time.|
    |Parallel queries are supported in the following scenarios:    -   Parallel queries are supported for cost models for range scans.
    -   Parallel queries are supported for temporary tables.
    -   Parallel queries can be performed based on the semi-join materialization strategies: lookup and scan. |
    |Three types of session state trackers are added. The PolarDB intelligent proxy can use these session state trackers for connection maintenance. After the trackers are enabled, you can track the changes of user variables in sessions, CREATE and DELETE operations on temporary tables, and PREPARE and DEALLOCATION operations in SQL statements.|
    |The performance of dropping an adaptive hash index \(AHI\) is optimized when DDL statements are executed. This reduces the impact of executing the DDL statements on instance performance.|
    |The recycle bin feature is added to avoid data loss that is caused by accidental deletion.|
    |The performance of truncating temporary tablespaces in large buffer pools is improved. This reduces the impact of the operations that are related to temporary tables on instance performance.|
    |Bugs fixed|The following bug is fixed: If aggregate functions are nested in the IF function, the bug occurs when the ROLLUP function is executed.|
    |This version fixes the bugs that are detected when the field values of the BLOB data type are sorted.|
    |This version fixes the bugs that are detected when the PREPARE statement includes aggregate functions in parallel queries.|
    |Several bugs that are related to parallel queries are fixed.|
    |The following bug is fixed: Excessive redo logs may be cleared.|
    |Bugs that are related to the redo logs of read-only nodes are fixed.|

-   8.0.1.1.1\(20200328\)

    |Category|Description|
    |--------|-----------|
    |Added features and performance optimization|If subqueries contain the ROLLUP function, parallel queries are supported.|
    |The statement concurrency control feature is supported.|
    |The `POLARDB_INDEX` hint is added.|
    |The replication delay between the primary node and read-only nodes is reduced.|
    |The thread pool feature is supported. For more information, see [Thread pool](/intl.en-US/User Guide/Kernel features/Features/Thread Pool.md).|
    |The keyring\_rds plug-in for Transparent Data Encryption \(TDE\) is supported.|
    |GDNs are supported. For more information, see [Global database networks](/intl.en-US/User Guide/Deployment Architecture/Global database networks/Create a GDN and a secondary cluster.md).|
    |The lock-free transaction system is optimized and the read and write performance is improved.|
    |Bugs fixed|Several bugs that are related to parallel queries are fixed.|
    |The following bug is fixed: The 0 value is returned for the statistics in online DDL operations.|
    |The file system in the user mode is optimized to accelerate instance startup.|
    |The following bug is fixed: Instances may become unavailable if innodb\_flush\_method is set to all\_o\_direct.|
    |The following bug is fixed: Instances may become unavailable if you release a lock after a transaction is committed.|
    |The following bug is fixed: User requests may be blocked when slow query logs are truncated.|
    |The following bug is fixed: Instances may become unavailable because of the compressed pages on read-only nodes.|
    |The following bug is fixed: Replication dump threads may be accidentally deleted in thread pools.|

-   8.0.1.1.0\(20200205\)

    |Category|Description|
    |--------|-----------|
    |Added features and performance optimization|The parallel query feature is improved, and the parallel computing of the ROLLUP function that is used for enterprise-level analysis is supported.|
    |The capabilities of the optimizer cost model are improved. You can specify filters to decrease selectivity. The cost model is supported for parallel queries. The optimizer determines whether a parallel or serial execution plan is used for the executed SQL statements based on the selectivity.|
    |Parallel threads that are allocated based on the first in, first out \(FIFO\) method. This ensures that system resources do not become exhaustive due to a large number of parallel queries.|
    |Bugs fixed|Memory-related bugs in parallel queries are fixed.|
    |Bugs that are related to instability in parallel queries are fixed.|

-   8.0.1.0.6\(20200101\)

    |Category|Description|
    |--------|-----------|
    |Bugs fixed|The following bug is fixed: The binary log index file is not closed after the primary node serves as a read-only node.|
    |The following bug is fixed: Instances become unavailable when read-only nodes access undo log pages that have been purged.|
    |The following bug is fixed: Background threads access tablespace pages that do not exist if a read-only node serves as the primary node.|
    |The following bug is fixed: After instances are shut down, log threads exit but redo logs are still being written. In this case, the instances become unavailable.|

-   8.0.1.0.5\(20191203\)

    |Category|Description|
    |--------|-----------|
    |Added features and performance optimization|The optimizer trace allows you to trace information about parallel queries. For example, you can use the optimizer trace to analyze the reason why a parallel query is used or not used.|
    |Hints are added for parallel queries. You can add hints to SQL statements to explicitly enable parallelism and specify the degree of parallelism.|
    |If you run the INSERT... SELECT statement when the isolation level is READ COMMITTED, parallel scans are supported. You can execute the INSERT... SELECT statement to query data and insert the result data into another table.|
    |Bugs fixed|Several bugs that are related to parallel queries are fixed.|
    |The following bug is fixed: Instances become unavailable during a failover between a read-only node and the primary node.|
    |The following bug is fixed: Errors are reported due to the execution of some DDL statements when a failover occurs.|
    |The following bug is fixed: An error message "too many connection error" is reported if the maximum number of connections that are supported by locks is reached.|


## PolarDB for MySQL 5.6 release notes

The following table describes the versions and the features that are supported by PolarDB for MySQL 5.6.

|Release date|Minor MySQL version that is fully compatible with PolarDB for MySQL|Released feature|
|------------|-------------------------------------------------------------------|----------------|
|20200616|5.6.16|The statement queue feature is supported. For more information, see [Statement Queue](/intl.en-US/User Guide/Kernel features/Optimization of SQL execution/Statement Queue.md).|
|20200601|5.6.16|The statement concurrency control feature is supported to improve concurrency performance. For more information, see [Statement Concurrency Control](/intl.en-US/User Guide/Kernel features/Optimization of SQL execution/Statement Concurrency Control.md).|
|20200507|5.6.16|The performance bottlenecks that are caused by internal data structures are removed. The simulated I/O system is optimized.|

-   5.6\(20200616\)

    |Category|Description|
    |--------|-----------|
    |Added features and performance optimization|The statement queue feature is supported. For more information, see [Statement Queue](/intl.en-US/User Guide/Kernel features/Optimization of SQL execution/Statement Queue.md).|
    |The replication delay between the primary node and read-only nodes is reduced.|
    |The metadata lock can be replicated when you execute the LOCK TABLE statement.|
    |Bugs fixed|Metadata lock bugs that occur during data replication are fixed.|
    |The following bug is fixed: An issue occurs when a full-text search \(FTS\) index is created in the system table.|
    |Bugs that are related to the updates and performance optimization operations of hot rows are fixed.|

-   5.6\(20200601\)

    |Category|Description|
    |--------|-----------|
    |Added features and performance optimization|Hot rows can be updated, and the performance of hot rows can be optimized. For more information, see [Hot row optimization](/intl.en-US/User Guide/Kernel features/Features/Hot row optimization.md).|
    |The statement concurrency control feature is supported. For more information, see [Statement Concurrency Control](/intl.en-US/User Guide/Kernel features/Optimization of SQL execution/Statement Concurrency Control.md).|
    |Bugs fixed|The following bug is fixed: The write performance is compromised due to the issues of thread pools.|

-   5.6\(20200507\)

    |Category|Description|
    |--------|-----------|
    |Added features and performance optimization|The statement concurrency control feature is added.|
    |A parameter is added to manage the rate of idle space to total space on index pages.|
    |The simulated AIO model is optimized.|
    |Bugs fixed|The following bug is fixed: The performance is compromised because the BoolFlag data type is used.|
    |The following bug is fixed: Instances become unavailable if the pfs\_umount table is not closed.|


## Version upgrade

-   Upgrade DB versions and minor versions

    PolarDB does not allow you to upgrade the DB versions and the minor versions in a direct way. For example, you cannot upgrade PolarDB for MySQL 5.6 to PolarDB for MySQL 8.0 or upgrade the minor version of PolarDB for MySQL from 8.0.1 to 8.0.2 in a direct way. However, to upgrade a version, you can use Data Transmission Service \(DTS\) to migrate or synchronize data from the cluster of the source version to the cluster of the destination version. For more information about how to migrate or synchronize data, see [Overview](/intl.en-US/Data Migration/Synchronization/Overview.md).

-   Upgrade revision versions

    For more information about how to upgrade revision versions, see [Upgrade the revision version](/intl.en-US/User Guide/Kernel features/Upgrade the revision version.md).


