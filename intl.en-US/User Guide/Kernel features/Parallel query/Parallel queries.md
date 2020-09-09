# Parallel queries

PolarDB for MySQL 8.0 launches a parallel query framework. If the amount of the queried data reaches a specific threshold, the parallel query framework is automatically enabled. This helps exponentially reduce query response time.

At the storage layer, data shards are distributed to different threads. Multiple threads perform parallel computing and return the results to the leader thread. Then, the leader thread merges the results and returns the final result. This helps improve the speed and accuracy of queries.

Parallel queries are achieved based on the parallel processing capabilities of multi-core CPUs. The following figure shows how parallel processing works on a node that has an 8-core CPU and 32 GB of memory.

![Diagram](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3329259951/p60483.png)

## Scenarios

Parallel queries are applicable to most SELECT statements, such as queries on large tables, multi-table queries that use JOINs, and queries that require a large amount of computing. The effect of parallel queries is not significant for short queries.

-   Lightweight analysis business

    Report queries are usually complex and time-consuming. The parallel query feature can accelerate a single query.

-   More available system resources

    Parallel queries consume more system resources. You can use the parallel query feature to improve resource utilization and query efficiency only when your system has more CPU resources, low I/O loads, and sufficient memory.

-   Combination of online and offline queries

    ![Combination of online and offline queries](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9930269951/p97221.png)

    You can use different endpoints to connect services to different database nodes. This prevents the services from affecting each other. If you enable the parallel query feature for a single-node endpoint, the read-only node that corresponds to the single-node endpoint is accessed over the endpoint that is used for online analytical processing \(OLAP\).


## Methods to use parallel queries

-   Use system parameters to control parallel queries

    PolarDB allows you to use the global parameter max\_parallel\_degree to specify the maximum number of threads that each SQL statement can use for parallel processing. The default value is 0. You can modify the parameter at any time when this parameter is in use. After you modify the parameter, you do not need to restart the database. For more information, see [Set cluster parameters](/intl.en-US/User Guide/Other operations/Set cluster parameters.md).

    We recommend that you configure the following parallel query settings:

    -   Increase the value of the max\_parallel\_degree parameter gradually. The value cannot exceed a quarter of CPU cores. Enable the parallel query feature only when your cluster has at least eight CPU cores. Do not enable the parallel query feature for small clusters. Set the max\_parallel\_degree parameter to 2 at the beginning when you use the parallel query feature. Check the CPU usage after a day of trial operation. If the CPU usage is not high, gradually increase the value. If the CPU usage is high, stop increasing the value.
    -   To disable the parallel query feature, set the max\_parallel\_degree parameter to 0. If the max\_parallel\_degree parameter is set to 1, the parallel query feature is enabled and the degree of parallelism \(DOP\) is 1.
    -   In the PolarDB console, the max\_parallel\_degree parameter is prefixed with loose and changes to loose\_max\_parallel\_degree. This allows the max\_parallel\_degree parameter to be applicable to other program versions, and follows the default settings of the max\_parallel\_degree parameter in the MySQL configuration files. This also ensures that programs of other versions can recognize the parameter and return no errors. For more information, see [Program Option Modifiers](https://dev.mysql.com/doc/refman/8.0/en/option-modifiers.html).
    -   When you enable the parallel query feature, set the innodb\_adaptive\_hash\_index parameter to OFF. If this parameter is set to ON, the parallel query performance is degraded.
    You can adjust the cluster-level DOP by modifying the global parameter. You can also adjust the DOP for SQL queries in a specific session. For example, if you add a session-level environment variable to the settings of the Java Database Connectivity \(JDBC\) connection string, you can set the DOP for a specific application.

    ```
    set max_parallel_degree = n 
    ```

-   Use hints

    You can optimize a single statement by using hints. For example, if the parallel query feature is disabled by the system, you can use hints to accelerate a slow SQL query that frequently runs.

    You can execute one of the following statements to enable the parallel query feature:

    ```
    SELECT /*+PARALLEL(x)*/ ... FROM ...;   -- x >0
    
    SELECT /*+ SET_VAR(max_parallel_degree=n) */  *  FROM ...   // n > 0
    ```

    You can execute one of the following statements to disable the parallel query feature:

    ```
    SELECT /*+NO_PARALLEL()*/ ... FROM ... ;
    
    SELECT /*+ SET_VAR(max_parallel_degree=0) */  *  FROM ...
    ```

    Advanced hint usage

    The parallel query feature supports two hints: PARALLEL and NO\_PARALLEL.

    -   You can use the PARALLEL hint to enforce parallel queries and specify the DOP and the table on which parallel scans are performed.
    -   You can use the NO\_PARALLEL hint to enforce serial queries or specify the tables for which parallel scans are prohibited.
    The following hint syntax is provided:

    ```
    /*+ PARALLEL [( [query_block] [table_name]  [degree] )] */
    /*+ NO_PARALLEL [( [query_block] [table_name][, table_name] )] */
    ```

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |query\_block|The name of the query block to which the hint is applied.|
    |table\_name|The name of the table to which the hint is applied.|
    |degree|The DOP.|

    Examples:

    ```
    SELECT /*+PARALLEL()*/ * FROM t1, t2; 
    -- The force_parallel_mode parameter is set to true. This indicates that parallel queries are forcibly executed even if the table contains less than 20,000 rows.
    -- The default parameter max_parallel_degree is used to specify the DOP. If max_parallel_degree is set to a value greater than 0, 
    -- parallel queries are enabled. If max_parallel_degree is set to 0, parallel queries are disabled.
    
    SELECT /*+PARALLEL(8)*/ * FROM t1, t2; 
    -- This statement enforces parallel queries in a DOP of 8. 
    -- The force_parallel_mode parameter is set to true. This indicates that parallel queries are forcibly executed even if the table contains less than 20,000 rows.
    -- The max_parallel_degree parameter is set to 8.
    
    SELECT /*+ SET_VAR(max_parallel_degree=8) */  *  FROM ...   
    -- The max_parallel_degree parameter is set to 8. 
    -- The force_parallel_mode parameter is set to false. This indicates that parallel queries are automatically disabled if the table contains less than 20,000 rows.
    
    SELECT /*+PARALLEL(t1)*/ * FROM t1, t2; 
    -- This statement enforces parallel queries on table t1 by using the /*+PARALLEL()*/ syntax for table t1.
    
    SELECT /*+PARALLEL(t1 8)*/ * FROM t1, t2; 
    -- This statement enforces parallel queries on table t1 in a DOP of 8 by using the /*+PARALLEL(8)*/ syntax for table t1.
    
    SELECT /*+PARALLEL(@subq1)*/ SUM(t.a) FROM t WHERE t.a = 
      (SELECT /*+QB_NAME(subq1)*/ SUM(t1.a) FROM t1); 
    -- This statement enforces parallel subqueries. The default parameter max_parallel_degree is used to specify the DOP. 
    -- If max_parallel_degree is set to a value greater than 0, parallel queries are enabled. If max_parallel_degree is set to 0, parallel queries are disabled.
    
    SELECT /*+PARALLEL(@subq1 8)*/ SUM(t.a) FROM t WHERE t.a = 
      (SELECT /*+QB_NAME(subq1)*/ SUM(t1.a) FROM t1); 
    -- This statement enforces parallel subqueries. The max_parallel_degree parameter is set to 8.
    
    SELECT SUM(t.a) FROM t WHERE t.a = 
      (SELECT /*+PARALLEL()*/ SUM(t1.a) FROM t1); 
    -- This statement enforces parallel subqueries. 
    -- The default parameter max_parallel_degree is used to specify the DOP. 
    -- If max_parallel_degree is set to a value greater than 0, parallel queries are enabled. If max_parallel_degree is set to 0, parallel queries are disabled.
    
    SELECT SUM(t.a) FROM t WHERE t.a = 
      (SELECT /*+PARALLEL(8)*/ SUM(t1.a) FROM t1); 
    -- This statement enforces parallel subqueries. The max_parallel_degree parameter is set to 8.
    
    
    
    SELECT /*+NO_PARALLEL()*/ * FROM t1, t2; 
    -- This statement prohibits parallel queries.
    
    SELECT /*+NO_PARALLEL(t1)*/ * FROM t1, t2; 
    -- This statement prohibits parallel queries for only table t1. If the system enables parallel queries, the system may perform parallel scans and run parallel queries on table t2.
    
    SELECT /*+NO_PARALLEL(t1, t2)*/ * FROM t1, t2; 
    -- This statement prohibits parallel queries for table t1 and table t2.
    
    SELECT /*+NO_PARALLEL(@subq1)*/ SUM(t.a) FROM t WHERE t.a = 
      (SELECT /*+QB_NAME(subq1)*/ SUM(t1.a) FROM t1); 
    -- This statement prohibits parallel subqueries.
    
    SELECT SUM(t.a) FROM t WHERE t.a = 
      (SELECT /*+NO_PARALLEL()*/ SUM(t1.a) FROM t1); 
     -- This statement prohibits parallel subqueries.
    ```

    **Note:** The PARALLEL hint is ineffective for queries that do not support parallel processing or tables that do not support parallel scans.

    You can also use hints to specify the policy to run parallel subqueries. For more information, see the support for subqueries in [Parallel execution plans](#section_8pu_06w_jw2). The following hint syntax is described:

    ```
    /*+ PQ_PUSHDOWN [( [query_block])] */ The subqueries run in parallel based on the pushdown policy.
    /*+ NO_PQ_PUSHDOWN [( [query_block])] */ The subqueries run in parallel based on the shared access policy.
    ```

    Examples:

    ```
    # The subqueries run in parallel based on the pushdown policy.
    EXPLAIN SELECT /*+ PQ_PUSHDOWN(@qb1) */ * FROM t2 WHERE t2.a =
                     (SELECT /*+ qb_name(qb1) */ a FROM t1);
    
    # The subqueries run in parallel based on the shared access policy.
    EXPLAIN SELECT /*+ NO_PQ_PUSHDOWN(@qb1) */ * FROM t2 WHERE t2.a =
                     (SELECT /*+ qb_name(qb1) */ a FROM t1);
    # No hint is added to the query block.
    EXPLAIN SELECT * FROM t2 WHERE t2.a =
                     (SELECT /*+ NO_PQ_PUSHDOWN() */ a FROM t1);
    ```

-   Force the optimizer to select parallel execution

    The PolarDB optimizer may not run queries in parallel. However, if you want the optimizer to ignore the cost and select parallel plans for most cases, you can set the following parameter:

    ```
    set force_parallel_mode = on
    ```

    **Note:** This is a debugging parameter. We recommend that you not use this parameter in production environments. Due to the limits of parallel query scenarios, in some cases, the optimizer may not run queries in parallel even if you specify this parameter.


## Parameters and variables

|Parameter|Level|Description|
|---------|-----|-----------|
|max\_parallel\_degree|Session and global|The maximum DOP for a single query. This indicates the maximum number of workers that are used to run queries in parallel.

-   Valid values: 0 to 1024
-   Default value: 0. This indicates that parallel computing is disabled.

**Note:** The PolarDB optimizer may use different parallel execution plans to run the main query and the subqueries in parallel. If the optimizer uses the same parallel execution plan to run the main query and the subqueries in parallel, the maximum number of workers cannot exceed the value of max\_parallel\_degree. The total number of workers is the sum of the number of workers used by the main query and those used by the subqueries. |
|force\_parallel\_mode|Session|Specifies whether to force the PolarDB optimizer to ignore the cost and use parallel queries for most cases.

-   Valid values: ON and OFF
-   Default value: OFF

**Note:** This is a debugging parameter. After you set the value to ON, the PolarDB optimizer may select parallel plans for most cases. However, the PolarDB optimizer may not use parallel queries. |

|Variable|Level|Description|
|--------|-----|-----------|
|Parallel\_workers\_created|Session and global|The number of parallel workers that have been generated since the start of the session.|
|Gather\_records|Session and global|The total number of records that are gathered.|
|PQ\_refused\_over\_memory\_soft\_limit|Session and global|The number of queries that are not run in parallel due to memory limits.|
|PQ\_refused\_over\_total\_workers|Session and global|The number of queries that are not run in parallel due to the limit on the total number of workers.|
|Total\_used\_query\_memory|Global|The amount of virtual memory that is used for the query.|
|Total\_running\_parallel\_workers|Global|The number of parallel workers that are running.|

## Performance metrics

The following tests use 100 GB of data that is generated based on TPC Benchmark™H \(TPC-H\) to test the performance metrics of a PolarDB for MySQL 8.0 cluster. In the tests, the cluster specification is a 32-core CPU and 256 GB of memory. The max\_parallel\_degree parameter is set to 32 for one of the two tests and 0 for the other test. For information about the test steps, see [OLAP performance tests](/intl.en-US/Performance White Paper/OLAP performance tests.md).

![Performance metrics](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3329259951/p97292.png)

The preceding figure shows that 95% of the SQL queries in TPC-H are accelerated. For 70% of the SQL queries, the query speed when the DOP is set to 32 is more than eight times faster than the query speed when the DOP is set to 0.

## Parallel execution plans

This section describes parallel query information in execution plans that are returned by the EXPLAIN statement.

-   Parallel scans

    In a parallel scan, workers simultaneously scan the data of a table. Each worker produces a partial result and returns the partial result to a leader thread. The leader thread gathers the results by using the Gather node and returns the final result to the client.

-   Parallel joins on multiple tables

    When parallel queries are enabled, the complete multi-table join operation is divided among workers for parallel processing. The PolarDB optimizer selects only the table that is considered to be optimal for parallel scanning. Non-parallel scanning is performed on all other tables. Each worker produces a partial result and returns the partial result to a leader thread. The leader thread gathers the results by using the Gather node and returns the final result to the client.

-   Parallel sorting

    The PolarDB optimizer divides the ORDER BY operation among workers for parallel processing. Each worker produces a partial result. The leader thread gathers, merges, and sorts all partial results by using the Gather Merge node, and returns the final sorting result to the client.

-   Parallel grouping

    The PolarDB optimizer divides the GROUP BY operation among workers for parallel processing. Each worker is responsible for the GROUP BY operation on a portion of the data. Each worker produces a partial result of GROUP BY. The leader thread gathers the results from all workers by using the Gather node. The PolarDB optimizer determines whether to perform a GROUP BY operation in the leader thread again based on the query plan. For example, if a loose index scan is used to run a GROUP BY query, the leader thread does not perform a GROUP BY operation. If the loose index scan is not used, the leader thread performs a GROUP BY operation and returns the final result to the client.

-   Parallel aggregation

    The execution of the aggregate function is divided among the parallel workers. PolarDB supports parallel aggregation in two stages. First, each worker that participates in the parallel portion of the query performs an aggregation step. Second, the leader thread gathers results from all workers by using the Gather or Gather Merge node. Finally, the leader thread re-aggregates the results from all workers to produce the final result.

-   Support for subqueries

    In parallel queries, subqueries can run by using one of the following policies:

    -   Serial execution in the leader thread

        If subqueries do not support parallel processing, the subqueries run in serial in the leader thread. For example, if two tables are joined by using a JOIN clause that references user-defined functions \(UDFs\), the subqueries run in serial.

    -   Parallel execution in the leader thread, which starts another group of workers to run parallel subqueries

        After a parallel plan is generated, the execution plan of the leader thread includes the subqueries that support parallel processing. However, these subqueries cannot run in parallel in advance or cannot run in parallel based on the shared access policy. For example, if the subqueries include window functions, the subqueries cannot run in parallel based on the shared access policy.

    -   Shared access

        After a parallel plan is generated, if the execution plans of workers reference the subqueries that support parallel processing, the PolarDB optimizer runs these subqueries in parallel in advance. This allows the workers to access the results of the subqueries in a direct way.

    -   pushed down

        After a parallel plan is generated, if the execution plans of workers reference correlated subqueries, the workers run these correlated subqueries.


## Examples of parallel execution plans

In the following example, the pq\_test table is used to test parallel queries.

Schema:

```
mysql> SHOW CREATE TABLE pq_test\G
*************************** 1. row ***************************
       Table: pq_test
Create Table: CREATE TABLE `pq_test` (
  `id` BIGINT(20) NOT NULL AUTO_INCREMENT,
  `help_topic_id` INT(10) UNSIGNED NOT NULL,
  `name` CHAR(64) NOT NULL,
  `help_category_id` SMALLINT(5) UNSIGNED NOT NULL,
  `description` TEXT NOT NULL,
  `example` TEXT NOT NULL,
  `url` TEXT NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=21495809 DEFAULT CHARSET=utf8
1 row in set (0.00 sec)
```

Table size:

```
mysql> SHOW TABLE STATUS\G
*************************** 1. row ***************************
           Name: pq_test
         Engine: InnoDB
        Version: 10
     Row_format: Dynamic
           Rows: 20064988
 Avg_row_length: 1898
    Data_length: 38085328896
Max_data_length: 0
   Index_length: 0
      Data_free: 4194304
 Auto_increment: 21495809
    Create_time: 2019-07-30 01:35:27
    Update_time: NULL
     Check_time: NULL
      Collation: utf8_general_ci
       Checksum: NULL
 Create_options:
        Comment:
1 row in set (0.02 sec)
```

SQL statement:

```
SELECT COUNT(*) FROM pq_test;
```

-   The EXPLAIN statement returns the following result when the parallel query is not used:

    ```
    mysql> SET max_parallel_degree=0; EXPLAIN SELECT COUNT(*) FROM pq_test\G
    Query OK, 0 rows affected (0.02 sec)
    *************************** 1. row ***************************
               Id: 1
      Select_type: SIMPLE
            Table: pq_test
      Partitions: NULL
             Type: index
    Possible_keys: NULL
              Key: PRIMARY
          Key_len: 8
              Ref: NULL
             Rows: 20064988
         Filtered: 100.00
            Extra: Using index
    1 row in set, 1 warning (0.03 sec)
    ```

-   The EXPLAIN statement returns the following result when the parallel query is used:

    ```
    mysql> EXPLAIN SELECT COUNT(*) FROM pq_test\G
    *************************** 1. row ***************************
               Id: 1
      Select_type: SIMPLE
            Table: &lt;gather2&gt;
       Partitions: NULL
             Type: ALL
    Possible_keys: NULL
              Key: NULL
          Key_len: NULL
              Ref: NULL
             Rows: 20064988
         Filtered: 100.00
            Extra: NULL
    *************************** 2. row ***************************
               Id: 2
      Select_type: SIMPLE
            Table: pq_test
       Partitions: NULL
             Type: index
    Possible_keys: NULL
              Key: PRIMARY
          Key_len: 8
              Ref: NULL
             Rows: 10032494
         Filtered: 100.00
            Extra: Parallel scan (2 workers); Using index
    2 rows in set, 1 warning (0.00 sec)
    ```

    The EXPLAIN output shows that the parallel plan includes a Gather operation. Gather is implemented to gather the partial results that are produced by all workers. In addition, information in the Extra field shows that a parallel scan is performed on the pq\_test table. This plan is expected to run a simultaneous scan by using two workers.

-   The EXPLAIN statement returns the following result when the parallel query is used for a statement that includes subqueries:

    ```
    mysql> EXPLAIN SELECT a, (select sum(t2.b) from t2 where t2.a = t1.b) FROM t1 WHERE (a, b) IN (SELECT b, MAX(a) FROM t2 GROUP BY b)\G
    *************************** 1. row ***************************
               id: 1
      select_type: PRIMARY
            table: <gather1>
       partitions: NULL
             type: ALL
    possible_keys: NULL
              key: NULL
          key_len: NULL
              ref: NULL
             rows: 2
         filtered: 100.00
            Extra: NULL
    *************************** 2. row ***************************
               id: 1
      select_type: PRIMARY
            table: t1
       partitions: NULL
             type: ALL
    possible_keys: NULL
              key: NULL
          key_len: NULL
              ref: NULL
             rows: 2
         filtered: 100.00
            Extra: Parallel scan (1 workers); Using where
    *************************** 3. row ***************************
               id: 2
      select_type: DEPENDENT SUBQUERY
            table: t2
       partitions: NULL
             type: ALL
    possible_keys: NULL
              key: NULL
          key_len: NULL
              ref: NULL
             rows: 2
         filtered: 50.00
            Extra: Parallel pushdown; Using where
    *************************** 4. row ***************************
               id: 3
      select_type: SUBQUERY
            table: <gather3>
       partitions: NULL
             type: ALL
    possible_keys: NULL
              key: NULL
          key_len: NULL
              ref: NULL
             rows: 1
         filtered: 100.00
            Extra: Shared access; Using temporary
    *************************** 5. row ***************************
               id: 3
      select_type: SIMPLE
            table: t2
       partitions: NULL
             type: ALL
    possible_keys: NULL
              key: NULL
          key_len: NULL
              ref: NULL
             rows: 2
         filtered: 100.00
            Extra: Parallel scan (1 workers); Using temporary
    5 rows in set, 2 warnings (0.02 sec)
    ```

    For the subquery whose select\_type is DEPENDENT SUBQUERY, the Extra field indicates the parallel pushdown policy. In the parallel pushdown policy, the subqueries are pushed down to workers for parallel processing. For the subquery whose select\_type is SBUQUERY, the Extra field indicates the shared access policy. In the shared access policy, the subqueries run in parallel in advance, and the result is shared among workers.


