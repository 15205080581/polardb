# ALTER TABLE… TRUNCATE SUBPARTITION {#concept_222020 .concept}

## 语法介绍 {#section_igm_35x_8z9 .section}

使用ALTER TABLE. TRUNCATE SUBPARTITION命令从指定的子分区中删除所有数据，留下完整的子分区结构。语法如下：

```
ALTER TABLE table_name 
  TRUNCATE SUBPARTITION subpartition_name 
  [{DROP|REUSE} STORAGE]
```

## 概述 {#section_96z_uwe_fk8 .section}

ALTER TABLE. TRUNCATE SUBPARTITION命令用于从指定的子分区中删除所有数据，留下完整的子分区结构。

ALTER TABLE. TRUNCATE SUBPARTITION不会引起可能因表而存在的触发器ON DELETE起火，但会使触发器ON TRUNCATE起火。如果为子分区定义了触发器ON TRUNCATE，那么就会使所有的触发器BEFORE TRUNCATE在截断操作前就起火，并使所有的触发器AFTER TRUNCATE在最后一个截断操作后也起火。

我们对一个表必须有TRUNCATE权限，才能调用ALTER TABLE. TRUNCATE SUBPARTITION。

## 参数 {#section_wwy_np4_3il .section}

|参数|参数说明|
|:-|:---|
|table name|分区表的名称（可以采用模式限定的方式引用）。|
|subpartition name|要截断的子分区名称。|

**说明：** 仅在兼容情况下包括DROP STORAGE 和 REUSE STORAGE子句，且子句会被解析并忽略。

## 示例 – 清空子分区 {#section_5v2_p7x_jjv .section}

下列示例从表sales的子分区中删除了数据。使用下列命令来创建表sales：

```
CREATE TABLE sales
(
  dept_no     number,
  part_no     varchar2,
  country     varchar2(20),
  date        date,
  amount      number
)
PARTITION BY RANGE(date) SUBPARTITION BY LIST (country)
(
  PARTITION "2011" VALUES LESS THAN('01-JAN-2012')
  (
    SUBPARTITION europe_2011 VALUES ('ITALY', 'FRANCE'),
    SUBPARTITION asia_2011 VALUES ('PAKISTAN', 'INDIA'),
    SUBPARTITION americas_2011 VALUES ('US', 'CANADA')
  ),
  PARTITION "2012" VALUES LESS THAN('01-JAN-2013')
  (
    SUBPARTITION europe_2012 VALUES ('ITALY', 'FRANCE'),
    SUBPARTITION asia_2012 VALUES ('PAKISTAN', 'INDIA'),
    SUBPARTITION americas_2012 VALUES ('US', 'CANADA')
  ),
  PARTITION "2013" VALUES LESS THAN('01-JAN-2015')
  (
    SUBPARTITION europe_2013 VALUES ('ITALY', 'FRANCE'),
    SUBPARTITION asia_2013 VALUES ('PAKISTAN', 'INDIA'),
    SUBPARTITION americas_2013 VALUES ('US', 'CANADA')
  )
);
```

使用下列命令填充表sales：

```
INSERT INTO sales VALUES
(10, '4519b', 'FRANCE', '17-Jan-2011', '45000'),
(20, '3788a', 'INDIA', '01-Mar-2012', '75000'),
(40, '9519b', 'US', '12-Apr-2012', '145000'),
(20, '3788a', 'PAKISTAN', '04-Jun-2012', '37500'),
(40, '4577b', 'US', '11-Nov-2012', '25000'),
(30, '7588b', 'CANADA', '14-Dec-2011', '50000'),
(30, '4519b', 'CANADA', '08-Apr-2012', '120000'),
(40, '3788a', 'US', '12-May-2011', '4950'),
(20, '3788a', 'US', '04-Apr-2012', '37500'),
(40, '4577b', 'INDIA', '11-Jun-2011', '25000'),
(10, '9519b', 'ITALY', '07-Jul-2012', '15000'),
(20, '4519b', 'INDIA', '2-Dec-2012', '5090');
```

查询表sales显示了记录已被分配在子分区之中：

```
acctg=# SELECT tableoid::regclass, * FROM sales;
      tableoid      | dept_no| part_no| country  |        date       |amount 
--------------------+--------+--------+----------+-------------------+-------
 sales_2011_europe  |      10| 4519b  | FRANCE   | 17-JAN-11 00:00:00|  45000
 sales_2011_asia    |      40| 4577b  | INDIA    | 11-JUN-11 00:00:00|  25000
 sales_2011_americas|      30| 7588b  | CANADA   | 14-DEC-11 00:00:00|  50000
 sales_2011_americas|      40| 3788a  | US       | 12-MAY-11 00:00:00|   4950
 sales_2012_europe  |      10| 9519b  | ITALY    | 07-JUL-12 00:00:00|  15000
 sales_2012_asia    |      20| 3788a  | INDIA    | 01-MAR-12 00:00:00|  75000
 sales_2012_asia    |      20| 3788a  | PAKISTAN | 04-JUN-12 00:00:00|  37500
 sales_2012_asia    |      20| 4519b  | INDIA    | 02-DEC-12 00:00:00|   5090
 sales_2012_americas|      40| 9519b  | US       | 12-APR-12 00:00:00| 145000
 sales_2012_americas|      40| 4577b  | US       | 11-NOV-12 00:00:00| 25000
 sales_2012_americas|      30| 4519b  | CANADA   | 08-APR-12 00:00:00| 120000
 sales_2012_americas|      20| 3788a  | US       | 04-APR-12 00:00:00|  37500
(12 rows)
```

要删除分区2012\_americas的内容，先要调用下列命令：

``` {#codeblock_rop_zu5_4v6}
ALTER TABLE sales TRUNCATE SUBPARTITION "americas_2 012";
```

现在，查询表sales显示了分区americas\_2012的内容已被删除：

```
acctg=# SELECT tableoid::regclass, * FROM sales;
      tableoid      | dept_no|part_no| country  |        date        | amount 
--------------------+--------+-------+----------+--------------------+-------
 sales_2011_europe  |      10| 4519b | FRANCE   | 17-JAN-11 00:00:00 |  45000
 sales_2011_asia    |      40| 4577b | INDIA    | 11-JUN-11 00:00:00 |  25000
 sales_2011_americas|      30| 7588b | CANADA   | 14-DEC-11 00:00:00 |  50000
 sales_2011_americas|      40| 3788a | US       | 12-MAY-11 00:00:00 |   4950
 sales_2012_europe  |      10| 9519b | ITALY    | 07-JUL-12 00:00:00 |  15000
 sales_2012_asia    |      20| 3788a | INDIA    | 01-MAR-12 00:00:00 |  75000
 sales_2012_asia    |      20| 3788a | PAKISTAN | 04-JUN-12 00:00:00 |  37500
 sales_2012_asia    |      20| 4519b | INDIA    | 02-DEC-12 00:00:00 |   5090
(8 rows)
```

当删除记录时，分区2012\_americas的结构仍然是完整的：

```
acctg=# SELECT subpartition_name, high_value FROM ALL_TAB_SUBPARTITIONS; 
 subpartition_name |     high_value      
-------------------+---------------------
 2013_europe       | 'ITALY', 'FRANCE'   
 2012_europe       | 'ITALY', 'FRANCE'   
 2011_europe       | 'ITALY', 'FRANCE'   
 2013_asia         | 'PAKISTAN', 'INDIA' 
 2012_asia         | 'PAKISTAN', 'INDIA' 
 2011_asia         | 'PAKISTAN', 'INDIA' 
 2013_americas     | 'US', 'CANADA'      
 2012_americas     | 'US', 'CANADA'      
 2011_americas     | 'US', 'CANADA'      
(9 
rows)
```

