# ALTER TABLE… TRUNCATE PARTITION {#concept_222014 .concept}

## 语法介绍 {#section_0k7_vfm_h14 .section}

使用ALTER TABLE. TRUNCATE PARTITION命令从指定的分区中删除数据，只留下完整的分区结构。语法如下：

```
ALTER TABLE table_name TRUNCATE PARTITION partition_name
  [{DROP|REUSE} STORAGE]
```

## 概述 {#section_co9_nnk_r3j .section}

使用ALTER TABLE. TRUNCATE PARTITION命令从指定的分区中删除数据，只留下完整的分区结构。当我们截断一个分区时，这个分区中的所有子分区也会被截断。

ALTER TABLE. TRUNCATE PARTITION不会引起可能因表而存在的触发器ON DELETE起火，但会使触发器ON TRUNCATE起火。如果为分区定义了触发器ON TRUNCATE，那么就会使所有的触发器BEFORE TRUNCATE在截断操作前就起火，并使所有的触发器AFTER TRUNCATE在最后一个截断操作后也起火。

我们必须对一个表有TRUNCATE权限，才能调用ALTER TABLE. TRUNCATE PARTITION。

## 参数 {#section_ike_j76_l85 .section}

|参数|参数说明|
|:-|:---|
|table name|分区表的名称（可以采用模式限定的方法引用）。|
|partition name|要删除的分区名称。|

**说明：** 仅在兼容情况下包括DROP STORAGE 和 REUSE STORAGE子句，且子句会被解析并忽略。

## 示例 – 清空分区 {#section_3jt_7ii_lln .section}

下列示例从表sales的一个分区中删除了数据。使用下列命令来创建表sales：

```
CREATE TABLE sales
(
  dept_no     number,   
  part_no     varchar2,
  country     varchar2(20),
  date        date,
  amount      number
)
PARTITION BY LIST(country)
(
  PARTITION europe VALUES('FRANCE', 'ITALY'),
  PARTITION asia VALUES('INDIA', 'PAKISTAN'),
  PARTITION americas VALUES('US', 'CANADA')
);
```

使用下列命令填充表sales：

```
INSERT INTO sales VALUES
(10, '4519b', 'FRANCE', '17-Jan-2012', '45000'),
(20, '3788a', 'INDIA', '01-Mar-2012', '75000'),
(40, '9519b', 'US', '12-Apr-2012', '145000'),
(20, '3788a', 'PAKISTAN', '04-Jun-2012', '37500'),
(40, '4577b', 'US', '11-Nov-2012', '25000'),
(30, '7588b', 'CANADA', '14-Dec-2012', '50000'),
(30, '9519b', 'CANADA', '01-Feb-2012', '75000'),
(30, '4519b', 'CANADA', '08-Apr-2012', '120000'),
(40, '3788a', 'US', '12-May-2012', '4950'),
(10, '9519b', 'ITALY', '07-Jul-2012', '15000'),
(10, '9519a', 'FRANCE', '18-Aug-2012', '650000'),
(10, '9519b', 'FRANCE', '18-Aug-2012', '650000'),
(20, '3788b', 'INDIA', '21-Sept-2012', '5090'),
(40, '4788a', 'US', '23-Sept-2012', '4950'),
(40, '4788b', 'US', '09-Oct-2012', '15000'),
(20, '4519a', 'INDIA', '18-Oct-2012', '650000'),
(20, '4519b', 'INDIA', '2-Dec-2012', '5090');
```

查询表sales显示了分区已由数据填充：

```
acctg=# SELECT tableoid::regclass, * FROM sales;
    tableoid    | dept_no | part_no | country  |        date        | amount 
----------------+---------+---------+----------+--------------------+--------
 sales_europe   |      10 | 4519b   | FRANCE   | 17-JAN-12 00:00:00 |  45000
 sales_europe   |      10 | 9519b   | ITALY    | 07-JUL-12 00:00:00 |  15000
 sales_europe   |      10 | 9519a   | FRANCE   | 18-AUG-12 00:00:00 | 650000
 sales_europe   |      10 | 9519b   | FRANCE   | 18-AUG-12 00:00:00 | 650000
 sales_asia     |      20 | 3788a   | INDIA    | 01-MAR-12 00:00:00 |  75000
 sales_asia     |      20 | 3788a   | PAKISTAN | 04-JUN-12 00:00:00 |  37500
 sales_asia     |      20 | 3788b   | INDIA    | 21-SEP-12 00:00:00 |   5090
 sales_asia     |      20 | 4519a   | INDIA    | 18-OCT-12 00:00:00 | 650000
 sales_asia     |      20 | 4519b   | INDIA    | 02-DEC-12 00:00:00 |   5090
 sales_americas |      40 | 9519b   | US       | 12-APR-12 00:00:00 | 145000
 sales_americas |      40 | 4577b   | US       | 11-NOV-12 00:00:00 |  25000
 sales_americas |      30 | 7588b   | CANADA   | 14-DEC-12 00:00:00 |  50000
 sales_americas |      30 | 9519b   | CANADA   | 01-FEB-12 00:00:00 |  75000
 sales_americas |      30 | 4519b   | CANADA   | 08-APR-12 00:00:00 | 120000
 sales_americas |      40 | 3788a   | US       | 12-MAY-12 00:00:00 |   4950
 sales_americas |      40 | 4788a   | US       | 23-SEP-12 00:00:00 |   4950
 sales_americas |      40 | 4788b   | US       | 09-OCT-12 00:00:00 |  15000
(17 rows)
```

要删除分区americas的内容，先要调用下列命令：

``` {#codeblock_qvg_qyh_e2h}
ALTER TABLE sales TRUNCATE PARTITION americas;
```

现在，查询表sales显示了分区americas的内容已被删除：

```
acctg=# SELECT tableoid::regclass, * FROM sales;
   tableoid   | dept_no | part_no | country  |        date        | amount 
--------------+---------+---------+----------+--------------------+--------
 sales_europe |      10 | 4519b   | FRANCE   | 17-JAN-12 00:00:00 |  45000
 sales_europe |      10 | 9519b   | ITALY    | 07-JUL-12 00:00:00 |  15000
 sales_europe |      10 | 9519a   | FRANCE   | 18-AUG-12 00:00:00 | 650000
 sales_europe |      10 | 9519b   | FRANCE   | 18-AUG-12 00:00:00 | 650000
 sales_asia   |      20 | 3788a   | INDIA    | 01-MAR-12 00:00:00 |  75000
 sales_asia   |      20 | 3788a   | PAKISTAN | 04-JUN-12 00:00:00 |  37500
 sales_asia   |      20 | 3788b   | INDIA    | 21-SEP-12 00:00:00 |   5090
 sales_asia   |      20 | 4519a   | INDIA    | 18-OCT-12 00:00:00 | 650000
 sales_asia   |      20 | 4519b   | INDIA    | 02-DEC-12 00:00:00 |   5090
(9 rows)
```

尽管删除了记录，分区americas的结构仍然是完整的：

```
acctg=# SELECT partition_name, high_value FROM ALL_TAB_PARTITIONS;
 partition_name |     high_value      
----------------+---------------------
 europe         | 'FRANCE', 'ITALY'   
 asia           | 'INDIA', 'PAKISTAN' 
 americas       | 'US', 'CANADA'      
(3 rows)
```

