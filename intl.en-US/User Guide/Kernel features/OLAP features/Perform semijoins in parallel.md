# Perform semijoins in parallel

You can use semijoins to optimize subqueries to reduce the number of queries and improve query performance. This topic describes the background information, the strategies, and the syntax of the semijoins. This topic also shows how to use the semijoins to improve query performance.

## Prerequisites

The PolarDB cluster version is PolarDB for MySQL 8.0 and the revision version is 8.0.1.1.2 or later.

## Background information

MySQL 5.6.5 introduces semijoins. If a row in an outer table matches one or more rows in an inner table, a semijoin returns the row from the outer table. The semijoin returns only the row from the outer table even if multiple rows are matched in the inner table. If regular subqueries are used, the regular subqueries run for all the tuples that meet the specified conditions in an outer table. This causes low efficiency of running the subqueries. In this case, you can use semijoins to optimize subqueries to reduce the number of queries and improve query performance. After semijions are used, inner tables are pulled out of subqueries to the FROM clauses of outer queries. Then, joins between the inner tables and the outer tables are performed. Therefore, the system returns query results if a tuple match is found between the inner tables and the outer tables. This improves query efficiency.

![1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8532729951/p133452.png)

## Semijoin strategies

The following semijoin strategies are supported:

-   DuplicateWeedout Strategy

    A temporary table that contains unique `row IDs` is created, and duplicates are removed based on the unique row IDs.

    ![2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8532729951/p133901.png)

-   Materialization Strategy

    The `nested tables` are materialized into an indexed temporary table that is used to perform a join. The index is used to remove duplicates.

    ![3](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8532729951/p133902.png)

-   Firstmatch Strategy

    This strategy shortcuts scanning after the first match is found. This removes duplicates.

    ![4](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9532729951/p133903.png)

-   LooseScan Strategy

    A subquery table is scanned based on an index. The index enables a single value to be chosen from the value group of each subquery. This removes duplicates.

    ![5](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9532729951/p133904.png)


## Syntax

Semijoins use the IN or EXISTS clause as join conditions.

-   ```
-- IN
SELECT *
FROM Employee
WHERE DeptName IN (
  SELECT DeptName
  FROM Dept
)
```

-   ```
-- EXISTS
SELECT *
FROM Employee
WHERE EXISTS (
  SELECT 1
  FROM Dept
  WHERE Employee.DeptName = Dept.DeptName
)
```


## Use parallel semijoins to improve query performance

PolarDB can implement all the four semijoin strategies in parallel to accelerate queries. In this way, semijoin tasks are split and a multi-thread model is used to run the task set in parallel. This improves the capabilities of removing duplicates and the query performance. TPC Benchmark™H \(TPC-H\) provides 22 SQL queries. In the following example, the twentieth SQL query is used.

```
select
s_name,
s_address
from
supplier, nation
where
s_suppkey in (
select
ps_suppkey
from
partsupp
where
ps_partkey in (
select
p_partkey
from
part
where
p_name like '[COLOR]%'
)
and ps_availqty > (
select
0.5 * sum(l_quantity)
from
lineitem
where
l_partkey = ps_partkey
and l_suppkey = ps_suppkey
and l_shipdate >= date('[DATE]')
and l_shipdate < date('[DATE]') + interval '1' year
)
)
and s_nationkey = n_nationkey
and n_name = '[NATION]'
order by
s_name;
```

In this example, the materialization is processed first and a degree of parallelism \(DOP\) of 32 is used. The materialized tables are used in the subsequent process. This makes full use of the processing capabilities of the CPUs and maximizes the parallel processing capabilities of outer queries. In the following execution plan, the parallel processing capabilities are achieved in the materialization and semijoin processes after parallel scans are used. In the following example, 1 GB of data that is represented by TPC-H scale factor 1 is used.

![2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9532729951/p133533.png)

The following figure shows the execution time of the statement when serial processing is used.

![1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9532729951/p136944.png)

The following figure shows the execution time of the statement when parallel scans are used.

![2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9532729951/p136945.png)

In the following custom SQL statements, parallel semijoins are used and the `max_parallel_degree` parameter is set to 32. In this case, the execution time of the statements is reduced from 2.59 seconds to 0.34 seconds.

```
mysql> SELECT c1,d1 FROM t1 WHERE c1 IN ( SELECT t2.c1 FROM t2 WHERE t2.c1 = 'f'      OR t2.c2 < 'y' ) and t1.c1 and d1 > '1900-1-1' like "R1%" ORDER BY t1.c1 DESC, t1.d1 DESC;
Empty set, 1024 warnings (0.34 sec)
mysql> set max_parallel_degree=0;
Query OK, 0 rows affected (0.00 sec)
mysql>  SELECT c1,d1 FROM t1 WHERE c1 IN ( SELECT t2.c1 FROM t2 WHERE t2.c1 = 'f'      OR t2.c2 < 'y' ) and t1.c1 and d1 > '1900-1-1' like "R1%" ORDER BY t1.c1 DESC, t1.d1 DESC;
Empty set, 65535 warnings (2.69 sec)
mysql> explain SELECT c1,d1 FROM t1 WHERE c1 IN ( SELECT t2.c1 FROM t2 WHERE t2.c1 = 'f'      OR t2.c2 < 'y' ) and t1.c1 and d1 > '1900-1-1' like "R1%" ORDER BY t1.c1 DESC, t1.d1 DESC;
+----+--------------+-------------+------------+--------+---------------+------------+---------+----------+--------+----------+---------------------------------------------------------+
| id | select_type  | table       | partitions | type   | possible_keys | key        | key_len | ref      | rows   | filtered | Extra                                                   |
+----+--------------+-------------+------------+--------+---------------+------------+---------+----------+--------+----------+---------------------------------------------------------+
|  1 | SIMPLE       | <gather1>   | NULL       | ALL    | NULL          | NULL       | NULL    | NULL     |  33464 |   100.00 | Merge sort                                              |
|  1 | SIMPLE       | t1          | NULL       | ALL    | NULL          | NULL       | NULL    | NULL     |  62802 |    30.00 | Parallel scan (32 workers); Using where; Using filesort |
|  1 | SIMPLE       | <subquery2> | NULL       | eq_ref | <auto_key>    | <auto_key> | 103     | sj.t1.c1 |      1 |   100.00 | NULL                                                    |
|  2 | MATERIALIZED | t2          | p0,p1      | ALL    | c1,c2         | NULL       | NULL    | NULL     | 100401 |    33.33 | Using where                                             |
+----+--------------+-------------+------------+--------+---------------+------------+------
```

