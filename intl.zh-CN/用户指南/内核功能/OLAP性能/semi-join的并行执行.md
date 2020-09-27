# semi-join的并行执行

您可以使用semi-join半连接优化子查询，减少查询次数，提高查询性能，本文将介绍semi-join半连接的基本信息和操作方法。

## 前提条件

PolarDB集群版本需为PolarDB MySQL 8.0且Revision version为8.0.1.1.2或以上。

## 背景信息

MySQL 5.6.5引入了semi-join半连接，当外表在内表中找到匹配的记录之后，semi-join会返回外表中的记录。但即使在内表中找到多条匹配的记录，外表也只会返回已经存在于外表中的记录。而对于子查询，父表的每个符合条件的元组都要执行一轮子查询，效率比较低下。此时使用半连接操作优化子查询，会减少查询次数，提高查询性能，其主要思路是将子查询上拉到父查询中，这样子查询的表和父查询中的表是并列关系，父表的每个符合条件的元组，只需要在子表中找符合条件的元组即可，所以效率会大大提高。

![1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2840359951/p133452.png)

## 策略

semi-join主要使用了如下策略：

-   DuplicateWeedout Strategy

    该策略创建由`row id`组成唯一ID的临时表，再通过该唯一ID达到去重目的。

    ![2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2840359951/p133901.png)

-   Materialization Strategy

    该策略将`nested tables`物化到临时表中，再通过查找物化表或者遍历物化表查找外表的方法达到去重目的。

    ![3](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2840359951/p133902.png)

-   Firstmatch Strategy

    该策略采用顺序查找表的方式，找到第一个匹配的记录后立即跳转到最后一个外表，并对外表的下一条记录执行JOIN操作，从而达到去重的目的

    ![4](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2840359951/p133903.png)

-   LooseScan Strategy

    该策略对内表基于索引（Index）进行分组，分组后与外表执行JOIN（进行Condition的匹配）操作，如果存在匹配的记录，则提取外表的记录，内表选取下一个分组继续进行计算，从而达到去重目的。

    ![5](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2840359951/p133904.png)


## 语法

semi-join通常使用IN或EXISTS作为连接条件。

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


## 并行semi-join性能提升

对于选择semi-join策略的查询，PolarDB对semi-join所有策略实现了并行加速，通过拆分semi-join的任务，多线程模型并行运行任务集，强化去重能力，使查询性能得到了显著的提升，以Q20为例。

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
and l_shipdate >= date('[DATE]’)
and l_shipdate < date('[DATE]’) + interval ‘1’ year
)
)
and s_nationkey = n_nationkey
and n_name = '[NATION]'
order by
s_name;
```

本文例子中将物化处理提前，并且以并行度（DOP）为32执行，后续的处理通过共享之前的物化表，同样充分发挥CPU的处理能力，将主查询的并行能力最大化，在如下的执行计划中，在标准TPCH SCALE为1G的数据量场景下，开启并行后，双层并行处理能力：

![2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2840359951/p133533.png)

在标准TPCH SCALE为1G的数据量场景下，串行的执行时间：

![1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3840359951/p136944.png)

并行开启情况下的执行时间：

![2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3840359951/p136945.png)

在如下自定义SQL并行中，使用了semi-join下推的并行方式，在`max_parallel_degree=32`的情况下，执行时间从2.59s减少到0.34s：

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

