# 在LIST 或 RANGE 分区表中处理偏离值 {#concept_222028 .concept}

分区或子分区DEFAULT 或 MAXVALUE会捕获任何不满足定义给表的其他分区规则的记录。

## 定义 DEFAULT 分区 {#section_hhw_8lx_0c2 .section}

分区DEFAULT会捕获那些在LIST分区（或子分区）表中不适用于任何其他分区的记录。如果我们不包括一个DEFAULT规则，那么任何不匹配分区约束中的其中一个值的记录都会导致错误。每个LIST分区或子分区可能会有自己的DEFAULT规则。

DEFAULT 规则的语法如下：

``` {#codeblock_22m_0m7_2z6}
PARTITION partition_name VALUES (DEFAULT)
```

其中partition\_name指定的是用于存储那些不匹配其他分区规则的记录的分区或子分区的名称。

最后的一个示例创建了列表分区表，在这个列表分区表中服务器会决定要存储基于列country值的数据的分区。如果我们试图添加一条记录，且这条记录中的列country值包含了一个没在规则中列出的值，那么POLARDB for Oracle就会报错：

```
acctg=# INSERT INTO sales VALUES
acctg-#   (40, '3000x', 'IRELAND', '01-Mar-2012', '45000');
ERROR:  inserted partition key does not map to any partition
```

下列示例创建了相同的表，但添加了一个DEFAULT分区。 服务器将存储那些不匹配在分区规则中指定的值的记录，其中这个分区规则是指定给分区others中的europe, asia, 或 americas分区的。

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
  PARTITION americas VALUES('US', 'CANADA'),
  PARTITION others VALUES (DEFAULT)
);
```

要测试分区DEFAULT，就要添加一条带有列country值的记录，且这个列country不与在分区约束中指定的任何一个国家匹配：

```
INSERT INTO sales VALUES
  (40, '3000x', 'IRELAND', '01-Mar-2012', '45000');
```

查询表sales的内容确认了之前被拒绝的记录现在是否存储在分区sales\_others中：

```
acctg=# SELECT tableoid::regclass, * FROM sales;
    tableoid    | dept_no | part_no | country  |        date        |  amount 
----------------+---------+---------+----------+--------------------+--------
 sales_europe   |      10 | 4519b   | FRANCE   | 17-JAN-12 00:00:00 |   45000
 sales_europe   |      10 | 9519b   | ITALY    | 07-JUL-12 00:00:00 |   15000
 sales_europe   |      10 | 9519a   | FRANCE   | 18-AUG-12 00:00:00 |  650000
 sales_europe   |      10 | 9519b   | FRANCE   | 18-AUG-12 00:00:00 |  650000
 sales_asia     |      20 | 3788a   | INDIA    | 01-MAR-12 00:00:00 |   75000
 sales_asia     |      20 | 3788a   | PAKISTAN | 04-JUN-12 00:00:00 |   37500
 sales_asia     |      20 | 3788b   | INDIA    | 21-SEP-12 00:00:00 |    5090
 sales_asia     |      20 | 4519a   | INDIA    | 18-OCT-12 00:00:00 |  650000
 sales_asia     |      20 | 4519b   | INDIA    | 02-DEC-12 00:00:00 |    5090
 sales_americas |      40 | 9519b   | US       | 12-APR-12 00:00:00 |  145000
 sales_americas |      40 | 4577b   | US       | 11-NOV-12 00:00:00 |   25000
 sales_americas |      30 | 7588b   | CANADA   | 14-DEC-12 00:00:00 |   50000
 sales_americas |      30 | 9519b   | CANADA   | 01-FEB-12 00:00:00 |   75000
 sales_americas |      30 | 4519b   | CANADA   | 08-APR-12 00:00:00 |  120000
 sales_americas |      40 | 3788a   | US       | 12-MAY-12 00:00:00 |    4950
 sales_americas |      40 | 4788a   | US       | 23-SEP-12 00:00:00 |    4950
 sales_americas |      40 | 4788b   | US       | 09-OCT-12 00:00:00 |   15000
 sales_others   |      40 | 3000x   | IRELAND  | 01-MAR-12 00:00:00 |   45000
(18 rows)
```

需要注意的是，POLARDB for Oracle并没有重新分配分区或子分区DEFAULT内容的方法。

-   我们不能使用ALTER TABLE, ADD PARTITION 命令把分区添加到带有DEFAULT 规则的表中，但我们可以使用ALTER TABLE ... SPLIT PARTITION 命令来划分现有的分区。
-   我们不能使用ALTER TABLE. ADD SUBPARTITION命令把子分区添加到带有DEFAULT 规则的表中，但我们可以使用ALTER TABLE. SPLIT SUBPARTITION命令来划分现有的子分区。

## 定义 MAXVALUE 分区 {#section_h2u_i47_adp .section}

分区或子分区MAXVALUE会捕获那些不适用于在范围分区或子分区表中的任何其他分区的记录。如果我们不包括MAXVALUE规则，那么任何超过分区规则所指定的最大限度的记录都会导致错误的产生。每个分区或子分区也许都有自己的MAXVALUE分区。

需要注意的是， POLARDB for Oracle并没有重新分配分区或子分区MAXVALUE内容的方法：

-   我们不能使用ALTER TABLE ... ADD PARTITION语句把分区添加到带有MAXVALUE规则的表中，但我们可以使用ALTER TABLE ... SPLIT PARTITION 语句来划分现有的分区。
-   我们不能使用ALTER TABLE. ADD SUBPARTITION语句把子分区添加到带有MAXVALUE规则的表中，但我们可以使用ALTER TABLE. SPLIT SUBPARTITION语句来划分现有的子分区。

MAXVALUE 规则的语法如下：

``` {#codeblock_54c_rpy_ehr}
PARTITION partition_name VALUES LESS THAN (MAXVALUE)
```

其中partition\_name指定的是用于存储那些不匹配其他分区规则的记录的分区名称。

最后的示例创建了一个范围分区表，且这个范围分区表中的数据是基于列date的值进行分区的。如果我们试图添加一条date值超过了分区约束中列出的日期值的记录，那么POLARDB for Oracle就会报错：

```
acctg=# INSERT INTO sales VALUES
acctg-#   (40, '3000x', 'IRELAND', '01-Mar-2013', '45000');
ERROR:  inserted partition key does not map to any partition
```

下列CREATE TABLE命令创建了相同的表，但这个表中是MAXVALUE分区。这时并没有产生错误，反而服务器会存储那些不匹配分区others中之前的分区约束的记录。

```
CREATE TABLE sales
(
  dept_no     number,
  part_no     varchar2,
  country     varchar2(20),
  date        date,
  amount      number
)
PARTITION BY RANGE(date)
(
  PARTITION q1_2012 VALUES LESS THAN('2012-Apr-01'),
  PARTITION q2_2012 VALUES LESS THAN('2012-Jul-01'),
  PARTITION q3_2012 VALUES LESS THAN('2012-Oct-01'),
  PARTITION q4_2012 VALUES LESS THAN('2013-Jan-01'),
  PARTITION others VALUES LESS THAN (MAXVALUE)
);
```

要测试分区MAXVALUE，就要添加一条带有列date值的记录，且这个列date 值还要超过在分区规则中列出的最后日期值。服务器将在分区others中存储这条记录：

``` {#codeblock_0wt_vn9_7e0}
INSERT INTO sales VALUES
                    (40, '3000x', 'IRELAND', '01-Mar-2 013', '45000');
                    '2 012-Apr-01 ' 2 012-Jul-01 ' 2 012-Oct-01 ' 2 013-Jan-01
```

查询表sales的内容确认了之前被拒绝的记录现在是否存储在分区sales\_others中：

```
acctg=# SELECT tableoid::regclass, * FROM sales;  
   tableoid    | dept_no | part_no | country  |        date        | amount 
---------------+---------+---------+----------+--------------------+---------
 sales_q1_2012 |      10 | 4519b   | FRANCE   | 17-JAN-12 00:00:00 |    45000
 sales_q1_2012 |      20 | 3788a   | INDIA    | 01-MAR-12 00:00:00 |    75000
 sales_q1_2012 |      30 | 9519b   | CANADA   | 01-FEB-12 00:00:00 |    75000
 sales_q2_2012 |      40 | 9519b   | US       | 12-APR-12 00:00:00 |   145000
 sales_q2_2012 |      20 | 3788a   | PAKISTAN | 04-JUN-12 00:00:00 |    37500
 sales_q2_2012 |      30 | 4519b   | CANADA   | 08-APR-12 00:00:00 |   120000
 sales_q2_2012 |      40 | 3788a   | US       | 12-MAY-12 00:00:00 |     4950
 sales_q3_2012 |      10 | 9519b   | ITALY    | 07-JUL-12 00:00:00 |    15000
 sales_q3_2012 |      10 | 9519a   | FRANCE   | 18-AUG-12 00:00:00 |   650000
 sales_q3_2012 |      10 | 9519b   | FRANCE   | 18-AUG-12 00:00:00 |   650000
 sales_q3_2012 |      20 | 3788b   | INDIA    | 21-SEP-12 00:00:00 |     5090
 sales_q3_2012 |      40 | 4788a   | US       | 23-SEP-12 00:00:00 |     4950
 sales_q4_2012 |      40 | 4577b   | US       | 11-NOV-12 00:00:00 |    25000
 sales_q4_2012 |      30 | 7588b   | CANADA   | 14-DEC-12 00:00:00 |    50000
 sales_q4_2012 |      40 | 4788b   | US       | 09-OCT-12 00:00:00 |    15000
 sales_q4_2012 |      20 | 4519a   | INDIA    | 18-OCT-12 00:00:00 |   650000
 sales_q4_2012 |      20 | 4519b   | INDIA    | 02-DEC-12 00:00:00 |     5090
 sales_others  |      40 | 3000x   | IRELAND  | 01-MAR-13 00:00:00 |    45000
(18 rows)
```

