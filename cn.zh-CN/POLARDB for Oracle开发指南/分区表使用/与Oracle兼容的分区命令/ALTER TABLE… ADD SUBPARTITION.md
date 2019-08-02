# ALTER TABLE… ADD SUBPARTITION {#concept_221763 .concept}

ALTER TABLE. ADD SUBPARTITION命令用于添加子分区到现有的分区中，且这个分区必须已经进行了子分区的划分。

## 语法介绍 {#section_29e_xnu_mzy .section}

使用ALTER TABLE. ADD SUBPARTITION命令添加一个子分区到现有的包含子分区的分区中。语法如下：

``` {#codeblock_bs2_ch8_owu}
ALTER TABLE table_name MODIFY PARTITION partition_name 
      ADD SUBPARTITION subpartition_definition;
```

其中 subpartition definition 是：

``` {#codeblock_0xl_i12_4m1}
{list subpartition | range subpartition}
```

list subpartition 是：

``` {#codeblock_noq_mkd_9xi}
SUBPARTITION [subpartition_name]
  VALUES (value[, value]...)
  [TABLESPACE tablespace_name]
```

range subpartition 是：

``` {#codeblock_i4q_22b_w1g}
SUBPARTITION subpartition_name
  VALUES LESS THAN (value[, value]...) 
  [TABLESPACE tablespace_name]
```

## 描述 {#section_oy6_4t1_o0e .section}

ALTER TABLE. ADD SUBPARTITION命令用于添加子分区到现有的分区中，且这个分区必须已经进行了子分区的划分。对于定义的子分区数量没有上限。

新的分区必须与现有分区的类型（LIST 或 RANGE）相同。新分区规则必须引用在（定义现有子分区的）子分区规则中指定的相同列。

您不能使用ALTER TABLE. ADD SUBPARTITION语句把分区添加到带有MAXVALUE或 DEFAULT规则的表中。但您可以用ALTER TABLE. SPLIT SUBPARTITION语句对现有子分区进行划分，有效地将子分区添加到表中。

您不能把新的子分区添加在范围子分区表中现有的子分区之前。 范围子分区必须以升序的方式指定。

包括TABLESPACE子句指定新的子分区要所属的表空间。如果您没有指定表空间， 那么子分区将创建于缺省表空间。

如果对表进行了索引设置， 那么索引将创建在新的子分区上。

要使用ALTER TABLE... ADD SUBPARTITION命令，您必须是表的拥有者或有超级用户（或管理员）的权限。

## 参数 {#section_c07_sjt_t37 .section}

|参数|参数说明|
|:-|:---|
|table name|子分区要所属的分区表名称（可以采用模式限定的方式引用）。|
|partition name|新的子分区要所属的分区名称。|
|subpartition name|要创建的子分区名称。子分区名称在所有分区和子分区中必须是唯一的，且必须遵循给对象标识符命名的惯例。|
|\(value\[, value\]...\)| 使用`value`来指定一个引用的文本值（或以逗号分隔的文本值列表）将表项目划分为不同的分区。每个分区规则必须至少指定一个值，但在规则中对于指定的值的数量没有上限要求。`Value`可能为`null`、`default` \(如果指定了一个`list`分区的话\) 或`maxvalue` \(如果指定了一个`range` 分区的话\)。

 更多关于创建`default`或`maxvalue`分区的信息请参见[在LIST 或 RANGE 分区表中处理偏离值](cn.zh-CN/POLARDB for Oracle开发指南/分区表使用/在LIST 或 RANGE 分区表中处理偏离值.md#)。

 |
|tablespace name|子分区所属的表空间名称。|

## 添加子分区到LIST-RANGE分区表示例 {#section_j8e_xbp_xut .section}

下列示例添加了一个RANGE子分区到列表分区表sales中。表sales是通过下列命令创建的：

``` {#codeblock_cv9_7e2_ok7}
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

表sales有三个分区，分别为europe、 asia 和 americas。每个分区都有两个范围定义的子分区：

``` {#codeblock_uax_uoe_40e}
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

下列命令添加了名为europe\_2013的子分区：

``` {#codeblock_18i_m58_igm}
ALTER TABLE sales MODIFY PARTITION europe 
  ADD SUBPARTITION europe_2013 
  VALUES LESS THAN('2015-Jan-01');
```

在调用命令这个命令之后，表包括了子分区europe\_2013：

``` {#codeblock_t9q_w8g_zp2}
acctg=# SELECT partition_name, subpartition_name, high_value FROM ALL_TAB_SUBPARTITIONS;
 partition_name | subpartition_name |  high_value   
----------------+-------------------+---------------
 europe         | europe_2011       | '2012-Jan-01' 
 europe         | europe_2012       | '2013-Jan-01' 
 europe         | europe_2013       | '2015-Jan-01' 
 asia           | asia_2011         | '2012-Jan-01' 
 asia           | asia_2012         | '2013-Jan-01' 
 americas       | americas_2011     | '2012-Jan-01' 
 americas       | americas_2012     | '2013-Jan-01' 
(7 rows)
```

需要注意的是，当添加一个新的范围子分区时，子分区规则必须指定一个范围，也就是说这个范围要在任何现有的子分区之后。

## 添加子分区到RANGE-LIST分区表示例 {#section_v2m_vr4_rzz .section}

下列示例添加了一个LIST子分区到RANGE分区表sales中。 表sales是通过下列命令创建的：

``` {#codeblock_kl7_ngd_bdq}
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
      SUBPARTITION europe VALUES ('ITALY', 'FRANCE'),
      SUBPARTITION americas VALUES ('US', 'CANADA')
    ),

    PARTITION second_half_2012 VALUES LESS THAN('01-JAN-2013') 
    (
      SUBPARTITION asia VALUES ('INDIA', 'PAKISTAN')
    )
  );
```

在执行上述命令之后，表sales将有两个分区，分别为first\_half\_2012和second\_half\_2012。分区first\_half\_2012又有两个子分区，分别为europe和americas；分区second\_half\_2012有一个分区，名为asia。

``` {#codeblock_lh1_43x_zko}
acctg=# SELECT partition_name, subpartition_name, high_value FROM ALL_TAB_SUBPARTITIONS;
  partition_name  | subpartition_name |     high_value      
------------------+-------------------+---------------------
 first_half_2012  | europe            | 'ITALY', 'FRANCE'  
 first_half_2012  | americas          | 'US', 'CANADA' 
 second_half_2012 | asia              | 'INDIA', 'PAKISTAN' 
(3 rows)
```

下列命令添加了一个名为east\_asia的子分区到分区second\_half\_2012中：

``` {#codeblock_p6n_3pn_1xr}
ALTER TABLE sales MODIFY PARTITION second_half_2012 
  ADD SUBPARTITION east_asia VALUES ('CHINA');
```

在调用这个命令后，表包括了子分区east\_asia：

``` {#codeblock_6hk_4nu_d6v}
acctg=# SELECT partition_name, subpartition_name, high_value FROM ALL_TAB_SUBPARTITIONS;
  partition_name  | subpartition_name |     high_value      
------------------+-------------------+---------------------
 first_half_2012  | europe            | 'ITALY', 'FRANCE'   
 first_half_2012  | americas          | 'US', 'CANADA'     
 second_half_2012 | asia              | 'INDIA', 'PAKISTAN' 
 second_half_2012 | east_asia         | 'CHINA'        
(4 rows)
```

