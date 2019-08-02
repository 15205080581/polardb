# CREATE TABLE...PARTITION BY {#concept_221638 .concept}

使用CREATE TABLE命令的PARTITION BY子句来创建一个分区表，这个分区表中的数据分配在一个或多个分区（和子分区）中。

## 语法介绍 {#section_0k9_ip6_dn3 .section}

CREATE TABLE命令语法有下面的四种形式：

-   列表分区语法

    使用第一种形式创建一个列表分区表：

    ``` {#codeblock_q3z_wxs_wt3}
    CREATE TABLE [ schema. ]table_name table definition PARTITION BY 
        LIST(column)
        [SUBPARTITION BY {RANGE|LIST} (column[, column ]...)] (list 
        partition definitionf, list partition definition]...);
    ```

    其中 list\_partition\_definition 是：

    ``` {#codeblock_0ud_lqj_tqt}
    PARTITION [partition_name] 
    VALUES (value[, value]...) [TABLESPACE tablespace_name] [(subpartition, ...)]
    ```

-   范围分区语法

    使用第二种形式创建范围分区表：

    ``` {#codeblock_dox_zw7_9g5}
    CREATE TABLE [ schema. ]table_name 
       table_definition
       PARTITION BY LIST(column)
       [SUBPARTITION BY {RANGE|LIST} (column[, column ]...)]
       (list_partition_definition[, list_partition_definition]...);
    ```

    其中 range partition definition 是：

    ``` {#codeblock_m25_4do_1uc}
    PARTITION [partition_name]
      VALUES (value[, value]...)
      [TABLESPACE tablespace_name]
      [(subpartition, ...)]
    ```

-   子分区语法

    subpartition 可能是下面两种的其中一种

    ``` {#codeblock_6ha_z6x_vwz}
    {list subpartition | range subpartition }
    ```

    其中 list\_subpartition 是：

    ``` {#codeblock_b25_kwl_661}
    SUBPARTITION [subpartition_name] VALUES (value[, value]...)
    [TABLESPACE tablespace_name]
    ```

    其中 range\_subpartition 是：

    ``` {#codeblock_vwd_pcs_omm}
    SUBPARTITION [subpartition_name]
    VALUES LESS THAN (value[, value]...) 
    [TABLESPACE tablespace_name] 
    ```


## 描述 {#section_qm5_v8o_f54 .section}

CREATE TABLE... PARTITION BY命令用于创建带有一个或多个分区的表，其中每个分区可能有一个或一个以上的子分区。对于定义的分区数量没有上限， 但如果您要包括PARTITION BY子句，则必须至少指定一个分区规则。产生的表由创建这个表的用户所有。

使用PARTITION BY LIST子句在指定列中输入的值的基础上对表进行分区。每个分区规则必须至少指定一个文本值，但对于您可能要指定的值的数量则没有上限。包括一个用于指定DEFAULT匹配值的规则将任何不符合的记录导入到指定的分区中。

使用PARTITION BY RANGE子句指定边界规则来创建分区。每个分区规则必须至少包含一列有两个运算符的数据类型（例如，一个大于等于运算符和一个小于运算符）。范围边界的评估是依据LESS THAN子句进行的，且范围边界是非包容性的。2013年1月1日这个日期边界只会包括那些在2012年12月31日当天及之前的日期值。

范围分区规则必须以升序方式指定。 如果INSERT命令存储的记录值超过了范围分区表的最大限制将会失败。除非分区规则中包括的边界规则指定了MAXVALUE值。如果您没有包括MAXVALUE分区规则，那么任何超过边界规则指定的最大限制的记录都会导致错误的产生。

使用关键字TABLESPACE指定分区或子分区要所属的表空间名称。如果您没有指定表空间， 那么分区或子分区则会所属于缺省表空间。

如果您使用CREATE TABLE语法在分区表上创建索引，那么这个索引也会同样创建于每个分区或子分区中。

如果表定义包括SUBPARTITION BY子句， 那么这个表中的每个分区都会有至少一个子分区。每个子分区可能是明确定义的或是系统定义的。

如果子分区是系统定义的，那么服务器产生的子分区将所属于缺省表空间中，且子分区的名称将由服务器指定。服务器会创建下列内容：

-   如果SUBPARTITION BY子句指定了LIST， 那么服务器会创建一个DEFAULT子分区。
-   如果SUBPARTITION BY子句指定了RANGE，那么服务器会创建一个MAXVALUE子分区。

服务器所产生的子分区名称是分区表名称与一个唯一标识符的结合。您可以查询表ALL\_TAB\_SUBPARTITIONS来检查完整的子分区名称列表。

## 参数 {#section_xur_rwg_ezv .section}

|参数|参数说明|
|:-|:---|
|table name|要创建的表名称（可以采用模式限定的方式引用）。|
|table definition|如在PostgreSQL核心文件中描述的那样，给`create table`语句的列名称、数据类型及约束信息请参考[createtable](http://www.enterprisedb.com/docs/en/9.3/pg/sql-createtable.html)。|
|partition name|要创建的分区名称。分区名称在所有分区和子分区中必须是唯一的，且必须遵循给对象标识符命名的惯例。|
|subpartition name|要创建的子分区名称。子分区名称在所有分区和子分区中必须是唯一的，且必须遵循给对象标识符命名的惯例。|
|column|分区规则所基于的列名称。 每条记录都将存储在一个符合于指定列值的分区中。|
|\(value\[, value\]...\)| 用`value`来指定一个引用的文本值（或以逗号分隔的文本值列表）将表项目划分为不同的分区。每个分区规则必须至少指定一个值，但在规则中对于指定的值的数量没有上限要求。`Value`可能为`null`、`default` \(如果指定了一个`list`分区的话\) 或`maxvalue` \(如果指定了一个`range` 分区的话\)。

 当给列表分区表指定规则时，要在最后的分区中包括关键字`default`来把任何不匹配的记录导入到指定分区中。如果您没有使用一个包括`default`值的规则，那么任何`insert`语句试图添加一条与（至少一个分区的）指定规则不匹配的记录都会失败，并返回错误。

 当给列表分区表指定规则时，在最后的分区规则中包括关键字`maxvalue`来把所有未分类的记录导入到指定分区中。如果包括`maxvalue`分区，那么在分区键大于指定最高值的情况下，`insert`语句试图添加记录的操作将会失败，并返回错误。

 |
|tablespace name|分区或子分区所属的表空间名称。|

## PARTITION BY LIST示例 {#section_y46_g01_6mw .section}

下列示例使用了PARTITION BY LIST子句创建了分区表（sales）。表sales在三个分区（europe、 asia 和 americas）中存储信息：

``` {#codeblock_sl4_d7a_eea}
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

在country列中指定的值对所产生的表进行了分区：

``` {#codeblock_9r1_p80_p08}
acctg=# SELECT partition_name, high_value from ALL_TAB_PARTITIONS;
 partition_name |     high_value      
----------------+---------------------
 americas       | 'US', 'CANADA'      
 asia           | 'INDIA', 'PAKISTAN' 
 europe         | 'FRANCE', 'ITALY'   
(3 rows)
```

-   Country列中带有US或CANADA值的记录存储于americas分区中。
-   Country列中带有INDIA 或 PAKISTAN值的记录存储于asia分区中。
-   Country列中带有FRANCE 或 ITALY值的记录存储于europe分区中。

服务器会依据分区规则对下列语句进行评估，并将记录存储在europe分区中：

``` {#codeblock_yeo_dli_xy4}
INSERT INTO sales VALUES (10, '9519a', 'FRANCE', '18-Aug-2012', '650000');
```

## PARTITION BY RANGE示例 {#section_w1m_8jk_vi9 .section}

下列示例使用了PARTITION BY RANGE子句创建了分区表（sales）。表sales在四个分区（q1\_2012、 q2\_2012、 q3\_2012 和 q4\_2012）中存储信息。

``` {#codeblock_p85_hnl_z7c}
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

在date列中指定的值对产生的表进行了分区。

``` {#codeblock_o43_rf1_5up}
acctg=# SELECT partition_name, high_value from ALL_TAB_PARTITIONS;
 partition_name |  high_value   
----------------+---------------
 q4_2012        | '2013-Jan-01' 
 q3_2012        | '2012-Oct-01' 
 q2_2012        | '2012-Jul-01' 
 q1_2012        | '2012-Apr-01' 
(4 rows)
```

-   在date列中任何带有2012年4月1日之前的值的记录都存储于q1\_2012分区中。
-   在date列中任何带有2012年7月1日之前的值的记录都存储于分区q2\_2012中。
-   在date列中任何带有2012年10月1日之前的值的记录都存储于分区q3\_2012中。
-   在date列中任何带有2013年1月1日之前的值的记录都存储于分区q4\_2012中。

服务器会依据分区规则对下列语句进行评估，并将记录存储在q3\_2012分区中。

``` {#codeblock_jb1_rr8_h7i}
INSERT INTO sales VALUES (10, '9519a', 'FRANCE', '18-Aug-2012', '650000');
```

## PARTITION BY RANGE, SUBPARTITION BY LIST示例 {#section_5pm_wbm_dte .section}

下列示例创建的分区表（sales）首先是通过事务日期进行分区。然后使用country列的值对范围分区（q1\_2012、 q2\_2012、 q3\_2012 和 q4\_2012）进行了列表子分区的划分。

``` {#codeblock_d1q_63q_y77}
CREATE TABLE sales
(
  dept_no     number,
  part_no     varchar2,
  country     varchar2(20),
  date        date,
  amount      number
)
PARTITION BY RANGE(date)
  SUBPARTITION BY LIST(country)
  (
    PARTITION q1_2012 
      VALUES LESS THAN('2012-Apr-01')
      (
        SUBPARTITION q1_europe VALUES ('FRANCE', 'ITALY'),
        SUBPARTITION q1_asia VALUES ('INDIA', 'PAKISTAN'),
        SUBPARTITION q1_americas VALUES ('US', 'CANADA')
       ),
  PARTITION q2_2012 
    VALUES LESS THAN('2012-Jul-01')
      (
        SUBPARTITION q2_europe VALUES ('FRANCE', 'ITALY'),
        SUBPARTITION q2_asia VALUES ('INDIA', 'PAKISTAN'),
        SUBPARTITION q2_americas VALUES ('US', 'CANADA')
       ),
  PARTITION q3_2012 
    VALUES LESS THAN('2012-Oct-01')
      (
        SUBPARTITION q3_europe VALUES ('FRANCE', 'ITALY'),
        SUBPARTITION q3_asia VALUES ('INDIA', 'PAKISTAN'),
        SUBPARTITION q3_americas VALUES ('US', 'CANADA')
       ),
  PARTITION q4_2012 
    VALUES LESS THAN('2013-Jan-01')
      (
        SUBPARTITION q4_europe VALUES ('FRANCE', 'ITALY'),
        SUBPARTITION q4_asia VALUES ('INDIA', 'PAKISTAN'),
        SUBPARTITION q4_americas VALUES ('US', 'CANADA')
       )
);
```

这条语句创建的表有四个分区。每个分区都有三个子分区：

``` {#codeblock_vd4_3cj_chd}
acctg=# SELECT subpartition_name, high_value, partition_name FROM ALL_TAB_SUBPARTITI0NS;
subpartition_name | high_value | partition_name     +    +    
q4_asia    | 'INDIA', 'PAKISTAN' | q4_2012
q4_europe    | 'FRANCE', 'ITALY' | q4_2012
SUBPARTITION q4_ SUBPARTITION q4_ SUBPARTITION q4_
q4_americas    | 'US', 'CANADA'    | q4_2012 
q3_americas    | 'US', 'CANADA'    | q3_2012 
q3_asia        | 'INDIA',         | q3_2012 
q3_europe    | 'PAKISTAN'         | q3_2012
q2_americas    | 'FRANCE', 'ITALY'    | q2_2012
q2_asia        | 'US', 'CANADA'    | q2_2012
q2_europe    | 'INDIA','PAKISTAN'     | q2_2012
q1_americas    | 'FRANCE', 'ITALY'    | q1_2012
q1_asia        | 'US', 'CANADA'     | q1_2012
q1_europe    | 'INDIA', 'PAKISTAN'     | q1_2012
12 rows)
```

当把记录添加到这个表中时，就会把date列中的值与在范围分区规则中指定的值进行比较，服务器会选择记录应该所属的分区。然后country列中的值就会与在列表子分区规则中指定的值相比较。当服务器定位了值的匹配信息时，记录就会存储在相应的子分区中。

任何添加到表中的记录都会存储在子分区中，因此所有的分区中都不会包含任何数据。

服务器会依据分区和子分区规则对下列语句进行评估，并将记录存储在q3\_europe分区中：

``` {#codeblock_1me_hx5_88q}
INSERT INTO sales VALUES (10, '9519a', 'FRANCE', '18-Aug-2012', '650000');
```

