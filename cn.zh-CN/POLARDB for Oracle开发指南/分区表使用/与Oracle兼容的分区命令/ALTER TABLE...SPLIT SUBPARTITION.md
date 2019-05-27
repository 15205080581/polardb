# ALTER TABLE...SPLIT SUBPARTITION {#concept_221802 .concept}

## 语法介绍 {#section_a9u_sax_lyw .section}

使用ALTER TABLE… SPLIT SUBPARTITION命令将一个子分区划分为两个子分区，并重新分配子分区的内容。ALTER TABLE… SPLIT SUBPARTITION命令有两种形式：

第一种形式将范围子分区划分为两个子分区：

``` {#codeblock_7sp_z83_qrx}
ALTER TABLE table_name SPLIT SUBPARTITION subpartition_name
  AT (range_part_value)
  INTO 
  (
    SUBPARTITION new_subpart1 
      [TABLESPACE tablespace_name],
    SUBPARTITION new_subpart2 
      [TABLESPACE tablespace_name]
  ); 
```

第二种形式将列表子分区划分为两个子分区：

``` {#codeblock_t1b_ipp_ej1}
ALTER TABLE table_name SPLIT SUBPARTITION subpartition_name
  VALUES (value[, value]...) 
  INTO 
  (
    SUBPARTITION new_subpart1 
      [TABLESPACE tablespace_name],
    SUBPARTITION new_subpart2 
      [TABLESPACE tablespace_name]
  );
```

## 描述 {#section_jtj_43p_6lc .section}

ALTER TABLE.. .SPLIT SUBPARTITION命令用于将子分区添加到现有的子分区表中。对于定义的子分区数量没有上限要求。当我们执行ALTER TABLE ...SPLIT SUBPARTITION命令时，POLARDB for Oracle会创建两个子分区，把所有包含（由指定子分区规则约束的）值的记录转移到new\_subpartl中，留下的其他记录则会转移到new\_subpart2中。

新分区规则必须引用在定义现有子分区的规则中指定的列。

包括TABLESPACE子句指定新的子分区要所属的表空间。如果我们没有指定表空间， 那么子分区将创建于缺省表空间。

如果对表进行了索引设置， 那么索引将创建在新的子分区上。

要使用ALTER TABLE.. . SPLIT SUBPARTITION命令，我们必须是表的拥有者或有超级用户 \(或管理员\) 的权限。

## 参数 {#section_2qq_rzd_7dj .section}

|参数|参数说明|
|:-|:---|
|table name|分区表名称（可以采用模式限定的方式引用）。|
|subpartition name|要划分的子分区名称。|
|new subpartl| 要创建的第一个新的子分区名称。在所有分区和子分区当中，子分区名称必须是唯一的，且必须遵循给对象标识符命名的惯例。

 `new_subpart1`会接收那些满足在`alter table... split subpartition`命令中指定的子分区约束的记录。

 |
|new subpart2| 要创建的第二个新的子分区名称。 在所有分区和子分区当中，子分区名称必须是唯一的，且必须遵循给对象标识符命名的惯例。

 `new_subpart2`会接收因`alter table. split``SUBPARTITION`命令指定的分区约束而未导入`new_subpartl`中的记录。

 |
|\(value\[, value\]...\)| 使用`value`来指定一个引用的文本值（或以逗号分隔的文本值列表）将表项目划分为不同的分区。每个分区规则必须至少指定一个值，但在规则中对于指定的值的数量没有上限要求。`Value`可能为`null`、`default` \(如果指定了一个`list`子分区的话\) 或`maxvalue` \(如果指定了一个`range` 子分区的话\)。

 更多关于创建`default` 或`maxvalue`分区的信息请参见[在LIST 或 RANGE 分区表中处理偏离值](cn.zh-CN/POLARDB for Oracle开发指南/分区表使用/在LIST 或 RANGE 分区表中处理偏离值.md#)。

 |
|tablespace name|分区或子分区所属的表空间名称。|

## 示例 – 划分LIST子分区 {#section_jax_pma_f1n .section}

下列示例划分了一个列表子分区，并重新分配了两个新的子分区之间的子分区内容。样本表\(sales\)是通过下列命令创建的：

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
  SUBPARTITION BY LIST (country)
  (
    PARTITION first_half_2012 VALUES LESS THAN('01-JUL-2012')
    (
      SUBPARTITION p1_europe VALUES ('ITALY', 'FRANCE'),
      SUBPARTITION p1_americas VALUES ('US', 'CANADA')
    ),
    PARTITION second_half_2012 VALUES LESS THAN('01-JAN-2013') 
    (
      SUBPARTITION p2_europe VALUES ('ITALY', 'FRANCE'),
      SUBPARTITION p2_americas VALUES ('US', 'CANADA')
    )
  );
```

表sales有两个分区，分别为first\_half\_2012 和second\_half\_2012。每个分区都有两个范围定义的子分区来把分区的内容分配到基于列country的值的子分区中。

``` {#codeblock_gtc_mts_q4o}
acctg=# SELECT partition_name, subpartition_name, high_value FROM ALL_TAB_SUBPARTITIONS;
  partition_name  | subpartition_name |    high_value     
------------------+-------------------+-------------------
 second_half_2012 | p2_europe         | 'ITALY', 'FRANCE' 
 first_half_2012  | p1_europe         | 'ITALY', 'FRANCE' 
 second_half_2012 | p2_americas       | 'US', 'CANADA'   
 first_half_2012  | p1_americas       | 'US', 'CANADA'  
(4 rows)
```

下面的命令添加了记录到每个子分区中：

``` {#codeblock_lff_8z5_f01}
INSERT INTO sales VALUES
  (10, '4519b', 'FRANCE', '17-Jan-2012', '45000'),
  (40, '9519b', 'US', '12-Apr-2012', '145000'),
  (40, '4577b', 'US', '11-Nov-2012', '25000'),
  (30, '7588b', 'CANADA', '14-Dec-2012', '50000'),
  (30, '9519b', 'CANADA', '01-Feb-2012', '75000'),
  (30, '4519b', 'CANADA', '08-Apr-2012', '120000'),
  (40, '3788a', 'US', '12-May-2012', '4950'),
  (10, '9519b', 'ITALY', '07-Jul-2012', '15000'),
  (10, '9519a', 'FRANCE', '18-Aug-2012', '650000'),
  (10, '9519b', 'FRANCE', '18-Aug-2012', '650000'),
  (40, '4788a', 'US', '23-Sept-2012', '4950'),
  (40, '4788b', 'US', '09-Oct-2012', '15000');
```

SELECT语句用于确认记录是否正确分配在所有子分区中：

``` {#codeblock_zzj_21t_1sx}
acctg=# SELECT tableoid::regclass, * FROM sales;
     tableoid      | dept_no | part_no | country|        date        |amount 
-------------------+---------+---------+--------+--------------------+------
 sales_p1_europe   |      10 | 4519b   | FRANCE | 17-JAN-12 00:00:00 |  45000
 sales_p1_europe   |      10 | 4519b   | FRANCE | 17-JAN-12 00:00:00 |  45000
 sales_p1_americas |      40 | 9519b   | US     | 12-APR-12 00:00:00 | 145000
 sales_p1_americas |      30 | 9519b   | CANADA | 01-FEB-12 00:00:00 |  75000
 sales_p1_americas |      30 | 4519b   | CANADA | 08-APR-12 00:00:00 | 120000
 sales_p1_americas |      40 | 3788a   | US     | 12-MAY-12 00:00:00 |   4950
 sales_p2_europe   |      10 | 9519b   | ITALY  | 07-JUL-12 00:00:00 |  15000
 sales_p2_europe   |      10 | 9519a   | FRANCE | 18-AUG-12 00:00:00 | 650000
 sales_p2_europe   |      10 | 9519b   | FRANCE | 18-AUG-12 00:00:00 | 650000
 sales_p2_americas |      40 | 4577b   | US     | 11-NOV-12 00:00:00 |  25000
 sales_p2_americas |      30 | 7588b   | CANADA | 14-DEC-12 00:00:00 |  50000
 sales_p2_americas |      40 | 4788a   | US     | 23-SEP-12 00:00:00 |   4950
 sales_p2_americas |      40 | 4788b   | US     | 09-OCT-12 00:00:00 |  15000
(13 rows)
```

下列命令将子分区p2\_americas划分为两个新的子分区，并重新分配了内容：

``` {#codeblock_pj0_ej9_t0t}
ALTER TABLE sales SPLIT SUBPARTITION p2_americas
  VALUES ('US') 
  INTO 
  (
    SUBPARTITION p2_us,
    SUBPARTITION p2_canada
  );
```

在调用这个命令后，子分区p2\_americas被删除。然后服务器在原有的这个位置创建了两个新的子分区\(p2\_us 和 p2\_canada\)：

``` {#codeblock_u5g_aar_zn8}
acctg=# SELECT partition_name, subpartition_name, high_value FROM ALL_TAB_SUBPARTITIONS;
  partition_name  | subpartition_name |    high_value     
------------------+-------------------+-------------------
 first_half_2012  | p1_europe         | 'ITALY', 'FRANCE' 
 first_half_2012  | p1_americas       | 'US', 'CANADA'    
 second_half_2012 | p2_europe         | 'ITALY', 'FRANCE' 
 second_half_2012 | p2_canada         | 'CANADA'          
 second_half_2012 | p2_us             | 'US'              
(5 rows)
```

对表sales的查询显示了子分区p2\_americas的内容已被重新分配：

``` {#codeblock_e7g_fii_eeu}
acctg=# SELECT tableoid::regclass, * FROM sales;
     tableoid      | dept_no | part_no | country |        date        |amount
-------------------+---------+---------+---------+--------------------+------
 sales_p1_europe   |      10 | 4519b   | FRANCE  | 17-JAN-12 00:00:00 | 45000
 sales_p1_europe   |      10 | 4519b   | FRANCE  | 17-JAN-12 00:00:00 | 45000
 sales_p1_americas |      40 | 9519b   | US      | 12-APR-12 00:00:00 |145000
 sales_p1_americas |      30 | 9519b   | CANADA  | 01-FEB-12 00:00:00 | 75000
 sales_p1_americas |      30 | 4519b   | CANADA  | 08-APR-12 00:00:00 |120000
 sales_p1_americas |      40 | 3788a   | US      | 12-MAY-12 00:00:00 |  4950
 sales_p2_europe   |      10 | 9519b   | ITALY   | 07-JUL-12 00:00:00 | 15000
 sales_p2_europe   |      10 | 9519a   | FRANCE  | 18-AUG-12 00:00:00 |650000
 sales_p2_europe   |      10 | 9519b   | FRANCE  | 18-AUG-12 00:00:00 |650000
 sales_p2_us       |      40 | 4577b   | US      | 11-NOV-12 00:00:00 | 25000
 sales_p2_us       |      40 | 4788a   | US      | 23-SEP-12 00:00:00 |  4950
 sales_p2_us       |      40 | 4788b   | US      | 09-OCT-12 00:00:00 | 15000
 sales_p2_canada   |      30 | 7588b   | CANADA  | 14-DEC-12 00:00:00 | 50000
(13 rows)
```

## 示例 – 划分 RANGE 子分区 {#section_rmh_84s_ysh .section}

下列示例划分了一个范围子分区，并重新分配了两个新的子分区之间的子分区内容。 样本表\(sales\)是通过下列命令创建的：

``` {#codeblock_999_g7e_vtr}
CREATE TABLE sales
(
  dept_no     number,   
  part_no     varchar2,
  country     varchar2(20),
  date        date,
  amount      number
)
PARTITION BY LIST(country)
  SUBPARTITION BY RANGE(date)
(
  PARTITION europe VALUES('FRANCE', 'ITALY')
    (
      SUBPARTITION europe_2011 
        VALUES LESS THAN('2012-Jan-01'),
      SUBPARTITION europe_2012 
        VALUES LESS THAN('2013-Jan-01')
    ),
  PARTITION asia VALUES('INDIA', 'PAKISTAN')
    (
      SUBPARTITION asia_2011 
        VALUES LESS THAN('2012-Jan-01'),
      SUBPARTITION asia_2012 
        VALUES LESS THAN('2013-Jan-01')
    ),
  PARTITION americas VALUES('US', 'CANADA')
    (
      SUBPARTITION americas_2011 
        VALUES LESS THAN('2012-Jan-01'),
      SUBPARTITION americas_2012 
        VALUES LESS THAN('2013-Jan-01')
    )
);
```

表sales有三个分区\(europe, asia, 和 americas\)。每个分区都有两个范围定义的子分区通过列date的值将分区内容分类并导入子分区中：

``` {#codeblock_e8z_krb_io6}
acctg=# SELECT partition_name, subpartition_name, high_value FROM ALL_TAB_SUBPARTITIONS;
 partition_name | subpartition_name |  high_value   
----------------+-------------------+---------------
 europe         | europe_2011       | '2012-Jan-01' 
 europe         | europe_2012       | '2013-Jan-01' 
 asia           | asia_2011         | '2012-Jan-01' 
 asia           | asia_2012         | '2013-Jan-01' 
 americas       | americas_2011     | '2012-Jan-01' 
 americas       | americas_2012     | '2013-Jan-01' 
(6 rows)
```

下列命令添加了记录到每个子分区中：

``` {#codeblock_hfs_v6t_fqr}
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

SELECT语句用于确认记录是否分配在子分区中：

``` {#codeblock_pvh_hrb_scq}
acctg=# SELECT tableoid::regclass, * FROM sales;
      tableoid       | dept_no|part_no| country |        date        |amount 
---------------------+--------+-------+---------+--------------------+---
 sales_europe_2012   |      10| 4519b | FRANCE  | 17-JAN-12 00:00:00 | 45000
 sales_europe_2012   |      10| 9519b | ITALY   | 07-JUL-12 00:00:00 | 15000
 sales_europe_2012   |      10| 9519a | FRANCE  | 18-AUG-12 00:00:00 | 650000
 sales_europe_2012   |      10| 9519b | FRANCE  | 18-AUG-12 00:00:00 | 650000
 sales_asia_2012     |      20| 3788a | INDIA   | 01-MAR-12 00:00:00 | 75000
 sales_asia_2012     |      20| 3788a | PAKISTAN| 04-JUN-12 00:00:00 | 37500
 sales_asia_2012     |      20| 3788b | INDIA   | 21-SEP-12 00:00:00 | 5090
 sales_asia_2012     |      20| 4519a | INDIA   | 18-OCT-12 00:00:00 | 650000
 sales_asia_2012     |      20| 4519b | INDIA   | 02-DEC-12 00:00:00 | 5090
 sales_americas_2012 |      40| 9519b | US      | 12-APR-12 00:00:00 | 145000
 sales_americas_2012 |      40| 4577b | US      | 11-NOV-12 00:00:00 | 25000
 sales_americas_2012 |      30| 7588b | CANADA  | 14-DEC-12 00:00:00 | 50000
 sales_americas_2012 |      30| 9519b | CANADA  | 01-FEB-12 00:00:00 | 75000
 sales_americas_2012 |      30| 4519b | CANADA  | 08-APR-12 00:00:00 | 120000
 sales_americas_2012 |      40| 3788a | US      | 12-MAY-12 00:00:00 | 4950
 sales_americas_2012 |      40| 4788a | US      | 23-SEP-12 00:00:00 | 4950
 sales_americas_2012 |      40| 4788b | US      | 09-OCT-12 00:00:00 | 15000
(17 rows)
```

下列命令将子分区americas\_2012划分为两个新的子分区，并重新分配了内容：

``` {#codeblock_796_7ly_j4l}
ALTER TABLE sales 
  SPLIT SUBPARTITION americas_2012 
  AT('2012-Jun-01')
  INTO
  (
    SUBPARTITION americas_p1_2012, 
    SUBPARTITION americas_p2_2012
  );
```

在调用这个命令之后，子分区americas\_2012被删除。然后服务器在原有的位置创建了两个新的子分区（americas\_p1\_2012和americas\_p2\_2012）：

``` {#codeblock_5kg_k0k_koz}
acctg=# SELECT partition_name, subpartition_name, high_value FROM ALL_TAB_SUBPARTITIONS;
 partition_name | subpartition_name |  high_value   
----------------+-------------------+---------------
 europe         | europe_2012       | '2013-Jan-01' 
 europe         | europe_2011       | '2012-Jan-01' 
 americas       | americas_2011     | '2012-Jan-01' 
 americas       | americas_p2_2012  | '2013-Jan-01' 
 americas       | americas_p1_2012  | '2012-Jun-01' 
 asia           | asia_2012         | '2013-Jan-01' 
 asia           | asia_2011         | '2012-Jan-01' 
(7 rows)
```

对表sales的查询显示了子分区的内容已被重新分配：

``` {#codeblock_zsa_an8_rpt}
acctg=# SELECT tableoid::regclass, * FROM sales;
      tableoid         | dept_no|part_no|country |      date         |amount 
-----------------------+--------+-------+--------+-------------------+------- sales_europe_2012      |      10| 4519b |FRANCE  | 17-JAN-12 00:00:00|  45000
 sales_europe_2012     |      10| 9519b |ITALY   | 07-JUL-12 00:00:00|  15000
 sales_europe_2012     |      10| 9519a |FRANCE  | 18-AUG-12 00:00:00| 650000
 sales_europe_2012     |      10| 9519b |FRANCE  | 18-AUG-12 00:00:00| 650000
 sales_asia_2012       |      20| 3788a |INDIA   | 01-MAR-12 00:00:00|  75000
 sales_asia_2012       |      20| 3788a |PAKISTAN| 04-JUN-12 00:00:00|  37500
 sales_asia_2012       |      20| 3788b |INDIA   | 21-SEP-12 00:00:00|   5090
 sales_asia_2012       |      20| 4519a |INDIA   | 18-OCT-12 00:00:00| 650000
 sales_asia_2012       |      20| 4519b |INDIA   | 02-DEC-12 00:00:00|   5090
 sales_americas_p1_2012|      40| 9519b |US      | 12-APR-12 00:00:00| 145000
 sales_americas_p1_2012|      30| 9519b |CANADA  | 01-FEB-12 00:00:00|  75000
 sales_americas_p1_2012|      30| 4519b |CANADA  | 08-APR-12 00:00:00| 120000
 sales_americas_p1_2012|      40| 3788a |US      | 12-MAY-12 00:00:00|   4950
 sales_americas_p2_2012|      40| 4577b |US      | 11-NOV-12 00:00:00|  25000
 sales_americas_p2_2012|      30| 7588b |CANADA  | 14-DEC-12 00:00:00|  50000
 sales_americas_p2_2012|      40| 4788a |US      | 23-SEP-12 00:00:00|   4950
 sales_americas_p2_2012|      40| 4788b |US      | 09-OCT-12 00:00:00|  15000
(17 rows)
```

