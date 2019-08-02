# ALTER TABLE… EXCHANGE PARTITION {#concept_221952 .concept}

ALTER TABLE...EXCHANGE PARTITION命令可以用一个分区或子分区交换现有的表。

## 语法介绍 {#section_c9v_1qz_zzb .section}

如果您打算添加大量的数据到分区表中，可以使用ALTER TABLE, EXCHANGE PARTITION命令来进行批量加载。您也可以使用ALTER TABLE. EXCHANGE PARTITION命令来删除旧数据或不再需要的数据。

ALTER TABLE. EXCHANGE PARTITION命令有以下两种形式。

-   第一种形式是把表换成分区：

    ``` {#codeblock_ajv_1in_cpd}
    ALTER TABLE target_table 
      EXCHANGE PARTITION target_partition 
      WITH TABLE source_table 
      [(WITH | WITHOUT) VALIDATION];
    ```

-   第二种形式是把表换成子分区 ：

    ``` {#codeblock_611_x3y_xkv}
    ALTER TABLE target_table 
      EXCHANGE SUBPARTITION target_subpartition 
      WITH TABLE source_table 
      [(WITH | WITHOUT) VALIDATION];
    ```


ALTER TABLE. EXCHANGE PARTITION命令在分区和子分区之间没有任何区别。

-   您可以使用EXCHANGE PARTITION或EXCHANGE SUBPARTITION子句来交换分区。
-   您可以使用EXCHANGE PARTITION或EXCHANGE SUBPARTITION子句来交换子分区。

## 描述 {#section_e94_b32_vf0 .section}

当完成ALTER TABLE. EXCHANGE PARTITION命令的执行后，最初在target\_partition中的数据就会位于source\_table中，而最初在source\_table中的数据则会位于target partition中。

source\_table的结构必须与target\_table的结构匹配（也就是说两个表必须有匹配的列和数据类型），且表内的数据必须依附分区约束。

POLARDB for Oracle接受WITHOUT VALIDATION子句，但会忽略。新表通常都是经过验证的。

您必须有一个表，才能基于这个表来调用ALTER TABLE. EXCHANGE PARTITION或ALTER TABLE. EXCHANGE SUBPARTITION。

## 参数 {#section_e3s_2sv_xuv .section}

|参数|参数说明|
|:-|:---|
|target table|分区所属的表名称（可以采用模式限定的方式引用）。|
|target partition|要替换的分区或子分区的名称。|
|source table|要替换`target_partition`的表名称。|

## 与表交换分区示例 {#section_sol_u0n_92u .section}

下面示例演示了把一个表换成了表sales中的分区（americas）的操作。您可以使用下列命令创建表sales：

``` {#codeblock_13i_1tp_dgr}
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

使用下列命令添加样本数据到表sales中：

``` {#codeblock_q76_iof_jk4}
INSERT INTO sales VALUES
  (40, '9519b', 'US', '12-Apr-2012', '145000'),
  (10, '4519b', 'FRANCE', '17-Jan-2012', '45000'),
  (20, '3788a', 'INDIA', '01-Mar-2012', '75000'),
  (20, '3788a', 'PAKISTAN', '04-Jun-2012', '37500'),
  (10, '9519b', 'ITALY', '07-Jul-2012', '15000'),
  (10, '9519a', 'FRANCE', '18-Aug-2012', '650000'),
  (10, '9519b', 'FRANCE', '18-Aug-2012', '650000'),
  (20, '3788b', 'INDIA', '21-Sept-2012', '5090'),
  (20, '4519a', 'INDIA', '18-Oct-2012', '650000'),
  (20, '4519b', 'INDIA', '2-Dec-2012', '5090');
```

查询表sales来显示分区americas中只有一条记录：

``` {#codeblock_gsu_vmx_ass}
acctg=# SELECT tableoid::regclass, * FROM sales;
    tableoid   | dept_no| part_no | country |      date     | amount 
---------------+--------+---------+---------+-------------------+-----------
 sales_europe  |      10| 4519b   | FRANCE  | 17-JAN-12 00:00:00|      45000
 sales_europe  |      10| 9519b   | ITALY   | 07-JUL-12 00:00:00|      15000
 sales_europe  |      10| 9519a   | FRANCE  | 18-AUG-12 00:00:00|     650000
 sales_europe  |      10| 9519b   | FRANCE  | 18-AUG-12 00:00:00|     650000
 sales_asia    |      20| 3788a   | INDIA   | 01-MAR-12 00:00:00|      75000
 sales_asia    |      20| 3788a   | PAKISTAN| 04-JUN-12 00:00:00|      37500
 sales_asia    |      20| 3788b   | INDIA   | 21-SEP-12 00:00:00|       5090
 sales_asia    |      20| 4519a   | INDIA   | 18-OCT-12 00:00:00|     650000
 sales_asia    |      20| 4519b   | INDIA   | 02-DEC-12 00:00:00|       5090
 sales_americas|      40| 9519b   | US      | 12-APR-12 00:00:00|     145000
(10 rows)
```

下列命令创建了一个与表sales定义匹配的表（n\_america）：

``` {#codeblock_to8_yjn_997}
CREATE TABLE n_america
(
  dept_no     number,   
  part_no     varchar2,
  country     varchar2(20),
  date    date,
  amount  number
);
```

下列命令添加了数据到表n\_america中。数据与分区americas的分区规则一致：

``` {#codeblock_yh0_qzp_cf5}
INSERT INTO n_america VALUES
  (40, '9519b', 'US', '12-Apr-2012', '145000'),
  (40, '4577b', 'US', '11-Nov-2012', '25000'),
  (30, '7588b', 'CANADA', '14-Dec-2012', '50000'),
  (30, '9519b', 'CANADA', '01-Feb-2012', '75000'),
  (30, '4519b', 'CANADA', '08-Apr-2012', '120000'),
  (40, '3788a', 'US', '12-May-2012', '4950'),
  (40, '4788a', 'US', '23-Sept-2012', '4950'),
  (40, '4788b', 'US', '09-Oct-2012', '15000');
```

下列命令将表换成分区表：

``` {#codeblock_c1q_etv_zh9}
ALTER TABLE sales 
  EXCHANGE PARTITION americas 
  WITH TABLE n_america; 
```

对表sales的查询显示了表n\_america中的内容已和分区americas中的内容交换：

``` {#codeblock_0jl_nkg_osw}
acctg=# SELECT tableoid::regclass, * FROM sales;
    tableoid   | dept_no| part_no | country |        date        | amount 
---------------+--------+--------+----------+--------------------+-----------
 sales_europe  |      10| 4519b   | FRANCE  | 17-JAN-12 00:00:00 |      45000
 sales_europe  |      10| 9519b   | ITALY   | 07-JUL-12 00:00:00 |      15000
 sales_europe  |      10| 9519a   | FRANCE  | 18-AUG-12 00:00:00 |     650000
 sales_europe  |      10| 9519b   | FRANCE  | 18-AUG-12 00:00:00 |     650000
 sales_asia    |      20| 3788a   | INDIA   | 01-MAR-12 00:00:00 |      75000
 sales_asia    |      20| 3788a   | PAKISTAN| 04-JUN-12 00:00:00 |      37500
 sales_asia    |      20| 3788b   | INDIA   | 21-SEP-12 00:00:00 |       5090
 sales_asia    |      20| 4519a   | INDIA   | 18-OCT-12 00:00:00 |     650000
 sales_asia    |      20| 4519b   | INDIA   | 02-DEC-12 00:00:00 |       5090
 sales_americas|      40| 9519b   | US      | 12-APR-12 00:00:00 |     145000
 sales_americas|      40| 4577b   | US      | 11-NOV-12 00:00:00 |      25000
 sales_americas|      30| 7588b   | CANADA  | 14-DEC-12 00:00:00 |      50000
 sales_americas|      30| 9519b   | CANADA  | 01-FEB-12 00:00:00 |      75000
 sales_americas|      30| 4519b   | CANADA  | 08-APR-12 00:00:00 |     120000
 sales_americas|      40| 3788a   | US      | 12-MAY-12 00:00:00 |       4950
 sales_americas|      40| 4788a   | US      | 23-SEP-12 00:00:00 |       4950
 sales_americas|      40| 4788b   | US      | 09-OCT-12 00:00:00 |      15000
(17 rows)
```

对表n\_america的查询显示了之前存储在分区americas中的记录已被移动到表n\_america中：

``` {#codeblock_ggi_qcq_53j}
acctg=# SELECT tableoid::regclass, * FROM n_america;
 tableoid  | dept_no | part_no | country |        date        | amount 
-----------+---------+---------+---------+--------------------+------------
 n_america |      40 | 9519b   | US      | 12-APR-12 00:00:00 |     145000
(1 row)
```

