# ALTER TABLE...SPLIT PARTITION {#concept_221780 .concept}

## 语法介绍 {#section_mob_imi_cfo .section}

使用ALTER TABLE. .. SPLIT PARTITION命令将一个分区划分为两个分区，并重新分配新分区的内容。ALTER TABLE. .. SPLIT PARTITION命令的语法有两种形式：

第一种形式用于将RANGE分区划分为两个分区：

``` {#codeblock_1hh_puc_s31}
ALTER TABLE table_name SPLIT PARTITION partition_name
  AT (range_part_value)
  INTO 
  (
    PARTITION new_part1 
      [TABLESPACE tablespace_name],
    PARTITION new_part2 
      [TABLESPACE tablespace_name]
  ); 
```

第二种形式用于将LIST分区划分为两个分区：

``` {#codeblock_kfy_a1p_oig}
ALTER TABLE table_name SPLIT PARTITION partition_name
  VALUES (value[, value]...) 
  INTO 
  (
    PARTITION new_part1 
      [TABLESPACE tablespace_name],
    PARTITION new_part2 
      [TABLESPACE tablespace_name]
  );
```

## 描述 {#section_so1_dq0_zha .section}

ALTER TABLE.. .SPLIT PARTITION命令用于将分区添加到现有的分区表中。在分区表中对于分区数量没有上限要求。

当我们执行ALTER TABLE ... SPLIT PARTITION命令时，POLARDB for Oracle就会创建两个新分区，并在这两个新分区之间（如分区规则约束的一样）重新分配旧分区中的内容。

包括TABLESPACE子句指定新分区要所属的表空间。如果我们没有指定表空间， 那么分区将所属于缺省表空间。

如果对表进行了索引设置， 那么索引将创建在新分区上。

要使用ALTER TABLE... SPLIT PARTITION命令，我们必须是表的拥有者或有超级用户\(或管理员\)的权限。

## 参数 {#section_k4j_hin_5tt .section}

|参数|参数说明|
|:-|:---|
|table name|分区表的名称（可以采用模式限定的方式引用）。|
|partition name|要划分的分区名称。|
|new parti| 要创建的第一个新分区的名称。在所有分区和子分区当中，分区名称必须是唯一的，且必须遵循给对象标识符命名的惯例。

 `new_parti`会接收那些满足在`alter table, split subpartition`命令中指定的子分区约束的记录。

 |
|new part2| 要创建的第二个新分区的名称。 在所有分区和子分区当中，分区名称必须是唯一的，且必须遵循给对象标识符命名的惯例。

 `new_part2`会接收因`alter table. split partition`命令指定的分区约束而未导入`new_parti`中的记录。

 |
|range part value|使用`range_part_value`指定边界规则来创建新分区。分区规则必须至少包含一列有两个运算符的数据类型（例如，一个大于等于运算符和一个小于运算符）。范围边界的评估是依据`less than`子句进行的，且范围边界是非包容性的。2010年1月1日这个日期边界只会包括那些在2009年12月31日当天或之前的日期值。|
|\(value\[, value\]...\)| 使用`value`来指定一个引用的文本值（或以逗号分隔的文本值列表）将记录分配到不同的分区中。每个分区规则必须至少指定一个值，但在规则中对于指定的值的数量没有上限要求。

 更多关于创建`default` 或`maxvalue`分区的信息请参见[在LIST 或 RANGE 分区表中处理偏离值](cn.zh-CN/POLARDB for Oracle开发指南/分区表使用/在LIST 或 RANGE 分区表中处理偏离值.md#)。

 |
|tablespace name|分区或子分区所属的表空间名称。|

## 示例 – 划分LIST分区 {#section_2pp_qok_hfl .section}

下面的示例将会把在列表分区表sales中的其中一个分区划分为两个新分区，并重新分配这两个分区的内容。表sales是通过下列语句创建的：

``` {#codeblock_h6j_c7s_r00}
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

表定义创建了三个分区\(europe, asia, 和 americas\)。下列命令添加了记录到每个分区中：

``` {#codeblock_lcg_sco_vbe}
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

在所有这些分区中分配记录：

``` {#codeblock_a6h_8pd_sm4}
acctg=# SELECT tableoid::regclass, * FROM sales;
    tableoid    | dept_no | part_no | country  |        date        | amount 
----------------+---------+---------+----------+--------------------+-------
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

下列命令将分区americas划分为两个分区，分别为us 和canada：

``` {#codeblock_pt4_29p_zpp}
ALTER TABLE sales SPLIT PARTITION americas 
  VALUES ('US')
  INTO (PARTITION us, PARTITION canada);
```

SELECT语句用于确认记录是否重新分配在正确的分区中：

``` {#codeblock_vk4_7lg_uhz}
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
 sales_us     |      40 | 9519b   | US       | 12-APR-12 00:00:00 | 145000
 sales_us     |      40 | 4577b   | US       | 11-NOV-12 00:00:00 |  25000
 sales_us     |      40 | 3788a   | US       | 12-MAY-12 00:00:00 |   4950
 sales_us     |      40 | 4788a   | US       | 23-SEP-12 00:00:00 |   4950
 sales_us     |      40 | 4788b   | US       | 09-OCT-12 00:00:00 |  15000
 sales_canada |      30 | 7588b   | CANADA   | 14-DEC-12 00:00:00 |  50000
 sales_canada |      30 | 9519b   | CANADA   | 01-FEB-12 00:00:00 |  75000
 sales_canada |      30 | 4519b   | CANADA   | 08-APR-12 00:00:00 | 120000
(17 rows)
```

## 示例 – 划分RANGE分区 {#section_iuy_u2u_ot4 .section}

下列示例将\(范围分区表sales的\)分区q4\_2012划分为两个分区， 并重新分配了分区的内容。使用下列命令创建表sales：

``` {#codeblock_c2i_mkp_uaf}
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
  PARTITION q1_2012 
    VALUES LESS THAN('2012-Apr-01'),
  PARTITION q2_2012 
    VALUES LESS THAN('2012-Jul-01'),
  PARTITION q3_2012 
    VALUES LESS THAN('2012-Oct-01'),
  PARTITION q4_2012 
    VALUES LESS THAN('2013-Jan-01')
);
```

表定义创建了四个分区 \(q1\_2012, q2\_2012, q3\_2012 q4\_2012\)。下列命令添加了记录到每个分区中：

``` {#codeblock_uhy_4m4_e2j}
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

SELECT语句用于确认记录是否按照预期那样分配在分区中：

``` {#codeblock_1m1_e8s_wit}
acctg=# SELECT tableoid::regclass, * FROM sales;
   tableoid    | dept_no | part_no | country  |        date        | amount 
---------------+---------+---------+----------+--------------------+--------
 sales_q1_2012 |      10 | 4519b   | FRANCE   | 17-JAN-12 00:00:00 |  45000
 sales_q1_2012 |      20 | 3788a   | INDIA    | 01-MAR-12 00:00:00 |  75000
 sales_q1_2012 |      30 | 9519b   | CANADA   | 01-FEB-12 00:00:00 |  75000
 sales_q2_2012 |      40 | 9519b   | US       | 12-APR-12 00:00:00 | 145000
 sales_q2_2012 |      20 | 3788a   | PAKISTAN | 04-JUN-12 00:00:00 |  37500
 sales_q2_2012 |      30 | 4519b   | CANADA   | 08-APR-12 00:00:00 | 120000
 sales_q2_2012 |      40 | 3788a   | US       | 12-MAY-12 00:00:00 |   4950
 sales_q3_2012 |      10 | 9519b   | ITALY    | 07-JUL-12 00:00:00 |  15000
 sales_q3_2012 |      10 | 9519a   | FRANCE   | 18-AUG-12 00:00:00 | 650000
 sales_q3_2012 |      10 | 9519b   | FRANCE   | 18-AUG-12 00:00:00 | 650000
 sales_q3_2012 |      20 | 3788b   | INDIA    | 21-SEP-12 00:00:00 |   5090
 sales_q3_2012 |      40 | 4788a   | US       | 23-SEP-12 00:00:00 |   4950
 sales_q4_2012 |      40 | 4577b   | US       | 11-NOV-12 00:00:00 |  25000
 sales_q4_2012 |      30 | 7588b   | CANADA   | 14-DEC-12 00:00:00 |  50000
 sales_q4_2012 |      40 | 4788b   | US       | 09-OCT-12 00:00:00 |   15000
 sales_q4_2012 |      20 | 4519a   | INDIA    | 18-OCT-12 00:00:00 | 650000
 sales_q4_2012 |      20 | 4519b   | INDIA    | 02-DEC-12 00:00:00 |   5090
(17 rows)
```

下列命令将分区q4\_2012划分为两个分区，分别为q4\_2012\_p1和q4\_2012\_p2：

``` {#codeblock_ftk_m9q_aha}
ALTER TABLE sales SPLIT PARTITION q4_2012
  AT ('15-Nov-2012')
  INTO 
  (
    PARTITION q4_2012_p1,
    PARTITION q4_2012_p2
  ); 
```

SELECT语句用于确认记录是否重新分配在新的分区中：

``` {#codeblock_cdt_l3v_irm}
acctg=# SELECT tableoid::regclass, * FROM sales;
     tableoid     | dept_no | part_no | country  |        date        |amount 
------------------+---------+---------+----------+--------------------+------
 sales_q1_2012    |      10 | 4519b   | FRANCE   | 17-JAN-12 00:00:00 | 45000
 sales_q1_2012    |      20 | 3788a   | INDIA    | 01-MAR-12 00:00:00 | 75000
 sales_q1_2012    |      30 | 9519b   | CANADA   | 01-FEB-12 00:00:00 | 75000
 sales_q2_2012    |      40 | 9519b   | US       | 12-APR-12 00:00:00 |145000
 sales_q2_2012    |      20 | 3788a   | PAKISTAN | 04-JUN-12 00:00:00 | 37500
 sales_q2_2012    |      30 | 4519b   | CANADA   | 08-APR-12 00:00:00 |120000
 sales_q2_2012    |      40 | 3788a   | US       | 12-MAY-12 00:00:00 |  4950
 sales_q3_2012    |      10 | 9519b   | ITALY    | 07-JUL-12 00:00:00 | 15000
 sales_q3_2012    |      10 | 9519a   | FRANCE   | 18-AUG-12 00:00:00 |650000
 sales_q3_2012    |      10 | 9519b   | FRANCE   | 18-AUG-12 00:00:00 |650000
 sales_q3_2012    |      20 | 3788b   | INDIA    | 21-SEP-12 00:00:00 |  5090
 sales_q3_2012    |      40 | 4788a   | US       | 23-SEP-12 00:00:00 |  4950
 sales_q4_2012_p1 |      40 | 4577b   | US       | 11-NOV-12 00:00:00 | 25000
 sales_q4_2012_p1 |      40 | 4788b   | US       | 09-OCT-12 00:00:00 | 15000
 sales_q4_2012_p1 |      20 | 4519a   | INDIA    | 18-OCT-12 00:00:00 |650000
 sales_q4_2012_p2 |      30 | 7588b   | CANADA   | 14-DEC-12 00:00:00 | 50000
 sales_q4_2012_p2 |      20 | 4519b   | INDIA    | 02-DEC-12 00:00:00 |  5090
(17 rows)
```

