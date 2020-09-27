# 并行查询中的hash join

本文介绍如何在PolarDB的并行查询中使用hash join功能。

## 前提条件

PolarDB集群版本需为PolarDB MySQL 8.0且Revision version为8.0.2.1.0或以上，您可以参见[查询版本号](/cn.zh-CN/.md)确认集群版本。

## 使用方法

-   语句

    目前在PolarDB中hash join只能通过`EXPLAIN FORMAT=TREE`语句来显示。

-   示例

    如下示例中创建了2个表，且在表里插入了一些数据：

    ```
    CREATE TABLE t1 (c1 INT, c2 INT);
    CREATE TABLE t2 (c1 INT, c2 INT);
    INSERT INTO t1 VALUES (1,1),(2,2),(3,3),(5,5);
    INSERT INTO t2 VALUES (1,1),(2,2),(3,3),(5,5);
    ```

    如下是上述2个表的JOIN的查询计划：

    ```
    EXPLAIN FORMAT=TREE
    
     EXPLAIN
     | -> Gather: 4 worker(s)  (cost=10.60 rows=4)
        -> Inner hash join (t2.c1 = t1.c1)  (cost=0.81 rows=1)
            -> Table scan on t2  (cost=0.09 rows=4)
            -> Hash
                -> Table scan on t1 with 0 parallel partitions  (cost=0.16 rows=1)
    ```

    上述是并行度为4的并行查询计划（即PolarDB会启用4个Worker来执行查询）。其中t1表会执行Parallel Scan，即由4个Worker分扫这个表，每个Worker使用t1的一部分数据建立各自的Hash表，再和整个t2表执行JOIN操作，最后收集（Gather）在Leader，得到整个查询的结果。


