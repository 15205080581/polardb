# Hash joins in parallel queries

This topic describes how to use hash joins in parallel queries in PolarDB.

## Prerequisites

The PolarDB cluster version is PolarDB for MySQL 8.0 and the revision version is 8.0.2.1.0 or later.

## Use hash joins in parallel queries

-   Statement

    PolarDB allows you to execute only the `EXPLAIN FORMAT=TREE` statement to check whether hash joins are used.

-   Examples

    In the following example, two tables are created and some data is inserted into the two tables.

    ```
    CREATE TABLE t1 (c1 INT, c2 INT);
    CREATE TABLE t2 (c1 INT, c2 INT);
    INSERT INTO t1 VALUES (1,1),(2,2),(3,3),(5,5);
    INSERT INTO t2 VALUES (1,1),(2,2),(3,3),(5,5);
    ```

    In the following example, the query plan for joining the preceding two tables is returned.

    ```
    EXPLAIN FORMAT=TREE
    
     EXPLAIN
     | -> Gather: 4 worker(s)  (cost=10.60 rows=4)
        -> Inner hash join (t2.c1 = t1.c1)  (cost=0.81 rows=1)
            -> Table scan on t2  (cost=0.09 rows=4)
            -> Hash
                -> Table scan on t1 with 0 parallel partitions  (cost=0.16 rows=1)
    ```

    In the preceding parallel query plan, the degree of parallelism \(DOP\) of 4 is used. This indicates that PolarDB uses four workers to perform parallel queries. Four workers scan table t1 in parallel. Each worker uses only part of data in table t1 to create a hash table. Then, a JOIN operation is performed between the four hash tables and table t2. A leader gathers the joined results to generate final query results.


