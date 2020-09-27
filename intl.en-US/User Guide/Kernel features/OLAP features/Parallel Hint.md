# Parallel Hint

The parallel hint feature allows you to specify whether the optimizer uses parallel processing. You can also specify a degree of parallelism \(DOP\) and tables on which parallel queries run. PolarDB supports two parallel hints: `PARALLEL` and `NO_PARALLEL`.

## Prerequisites

The PolarDB cluster version is PolarDB for MySQL 8.0 and the revision version is 8.0.1.0.5 or later.

## PARALLEL Hint

You can use the following syntax to add the PARALLEL hint to your SQL statement to enforce parallel queries. You can also specify the DOP and the table on which parallel queries run.

```
/*+ parallel [( [query_block] [table_name]  [degree] )] */
```

Examples

-   Enforce parallel queries.

    ```
    SELECT /*+PARALLEL()*/ * FROM t1, t2;
    ```

-   Enforce parallel queries in a DOP of 8.

    ```
    SELECT /*+PARALLEL(8)*/ * FROM t1, t2;
    ```

-   Enforce parallel queries on table t1.

    ```
    SELECT /*+PARALLEL(t1)*/ * FROM t1, t2;
    ```

-   Enforce parallel queries on table t1 in a DOP of 8.

    ```
    SELECT /*+PARALLEL(t1 8)*/ * FROM t1, t2;
    ```


**Note:**

-   You can set the DOP to 1024 at most.
-   You can specify only one table on which parallel queries run.
-   If the specified table does not exist, the system ignores the hint and displays a `Warning` message.
-   If the specified table does not support parallel queries, the system ignores the hint.

## NO\_PARALLEL hint

You can use the following syntax to add the NO\_PARALLEL hint to your statement to enforce serial queries. You can also specify the tables for which parallel queries are prohibited.

-   Enforce serial queries.

    ```
    SELECT /*+NO_PARALLEL()*/ * FROM t1, t2;
    ```

-   Prohibit parallel queries for table t1.

    ```
    SELECT /*+NO_PARALLEL(t1)*/ * FROM t1, t2;
    ```

-   Prohibit parallel queries for tables t1 and t2.

    ```
    SELECT /*+NO_PARALLEL(t1, t2)*/ * FROM t1, t2;
    ```


**Note:**

-   If the specified tables do not exist, the system ignores the hint and displays a `Warning` message.
-   If you prohibit parallel queries for all the tables, all the tables are queried in serial.

