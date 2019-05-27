# TRUNCATE TABLE {#concept_222007 .concept}

## 语法介绍 {#section_bea_oes_gf1 .section}

在保留表定义时，我们可以使用TRUNCATE TABLE 命令来删除表的内容。当我们截断表时，表中所有的分区或子分区也会被截断。语法如下：

``` {#codeblock_78e_7aw_3b6}
TRUNCATE TABLE table_name;
```

## 概述 {#section_b4y_2eo_gub .section}

TRUNCATE TABLE命令用于删除整个表及表内的所有数据。当删除表时，这个表内的所有分区或子分区也会被删除。

要使用TRUNCATE TABLE 命令，我们必须是分区的拥有者、拥有表的小组成员、模式的拥有者或是数据库的超级用户。

## 参数 {#section_yf4_9md_wuo .section}

|参数|参数说明|
|:-|:---|
|table name|分区表的名称（可以采用模式限定的方式引用）。|

## 示例 – 清空表 {#section_nmo_lgn_yma .section}

下列示例从表sales中删除了数据。使用下列命令来创建表sales：

```
CREATE TABLE sales
(
  dept_no     number,   
  part_no     varchar2,
  country     varchar2(20),
  date    date,
  amount  number
)
PARTITION BY LIST(country)
(
  PARTITION europe VALUES('FRANCE', 'ITALY'),
  PARTITION asia VALUES('INDIA', 'PAKISTAN'),
  PARTITION americas VALUES('US', 'CANADA')
);
```

使用下面这条命令填充表sales：

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

查询表sales 显示了分区由数据填充：

```
acctg=# SELECT tableoid::regclass, * FROM sales;
   tableoid   |dept_no | part_no | country  |        date        | amount 
--------------+--------+---------+----------+--------------------+-----------
sales_europe  |     10 | 4519b   | FRANCE   | 17-JAN-12 00:00:00 |     45000
sales_europe  |     10 | 9519b   | ITALY    | 07-JUL-12 00:00:00 |     15000
sales_europe  |     10 | 9519a   | FRANCE   | 18-AUG-12 00:00:00 |    650000
 sales_europe |     10 | 9519b   | FRANCE   | 18-AUG-12 00:00:00 |    650000
sales_asia    |     20 | 3788a   | INDIA    | 01-MAR-12 00:00:00 |     75000
sales_asia    |     20 | 3788a   | PAKISTAN | 04-JUN-12 00:00:00 |     37500
sales_asia    |     20 | 3788b   | INDIA    | 21-SEP-12 00:00:00 |      5090
sales_asia    |     20 | 4519a   | INDIA    | 18-OCT-12 00:00:00 |    650000
sales_asia    |     20 | 4519b   | INDIA    | 02-DEC-12 00:00:00 |      5090
sales_americas|     40 | 9519b   | US       | 12-APR-12 00:00:00 |    145000
sales_americas|     40 | 4577b   | US       | 11-NOV-12 00:00:00 |     25000
sales_americas|     30 | 7588b   | CANADA   | 14-DEC-12 00:00:00 |     50000
sales_americas|     30 | 9519b   | CANADA   | 01-FEB-12 00:00:00 |     75000
sales_americas|     30 | 4519b   | CANADA   | 08-APR-12 00:00:00 |    120000
sales_americas|     40 | 3788a   | US       | 12-MAY-12 00:00:00 |      4950
sales_americas|     40 | 4788a   | US       | 23-SEP-12 00:00:00 |      4950
sales_americas|     40 | 4788b   | US       | 09-OCT-12 00:00:00 |     15000
(17 rows)
```

要删除表sales 的内容，先要调用下列命令：

``` {#codeblock_9oh_k8y_nw0}
TRUNCATE TABLE sales; 
```

现在，查询表sales表明数据 已被删除，但结构是完整的：

```
acctg=# SELECT tableoid::regclass, * FROM sales;
 tableoid | dept_no | part_no | country |   date   | amount 
----------+---------+---------+---------+----------+------------
(0 rows)
```

更多关于TRUNCATE TABLE命令的信息，请参见[TRUNCATE](https://www.enterprisedb.com/docs/en/9.3/pg/sql-truncate.html)。

