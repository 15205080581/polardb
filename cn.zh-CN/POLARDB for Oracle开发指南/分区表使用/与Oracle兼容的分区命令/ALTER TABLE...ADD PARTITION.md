# ALTER TABLE...ADD PARTITION {#concept_221764 .concept}

## 语法介绍 {#section_105_owx_hnw .section}

使用ALTER TABLE. .. ADD PARTITION命令把分区添加到现有的分区表中。语法如下：

``` {#codeblock_66k_9b0_hl4}
ALTER TABLE table_name ADD PARTITION partition_definition;
```

其中 partition\_definition 是：

``` {#codeblock_3rr_am4_1if}
{list partition | range partition}
```

list\_partition 是：

``` {#codeblock_mrn_jlp_km4}
PARTITION [partition_name]
  VALUES (value[, value]...)
  [TABLESPACE tablespace_name]
  [(subpartition, ...)]
```

range partition 是：

``` {#codeblock_w7t_16v_pos}
PARTITION [partition_name]
  VALUES LESS THAN (value[, value]...)
  [TABLESPACE tablespace_name]
  [(subpartition, ...)]
```

其中 subpartition 是：

``` {#codeblock_d8o_vez_ebq}
{list subpartition | range subpartition}
```

list subpartition 是：

``` {#codeblock_brv_br4_nw2}
SUBPARTITION [subpartition_name]
  VALUES (value[, value]...)
  [TABLESPACE tablespace_name]
```

range subpartition 是：

``` {#codeblock_0og_9rw_r8m}
SUBPARTITION [subpartition_name ]
  VALUES LESS THAN (value[, value]...)
  [TABLESPACE tablespace_name]
```

## 描述 {#section_s2o_vc0_4i3 .section}

ALTER TABLE... ADD PARTITION命令用于将分区添加到现有的分区表中。在分区表中对于定义的分区数量没有上限。

新的分区必须与现有分区的类型\(LIST or RANGE\)相同。新分区规则必须引用和定义现有分区的分区规则中指定的相同列。

我们不能使用ALTER TABLE... ADD PARTITION语句把分区添加到带有MAXVALUE或 DEFAULT规则的表中。需要注意的是，我们可以交替使用ALTER TABLE. SPLIT PARTITION语句对现有分区进行划分，有效增加表中的分区数量。

RANGE分区必须以升序的方式指定。我们不能把新分区添加在RANGE分区表中现有的分区之前。

包括TABLESPACE子句指定新分区要所属的表空间。如果我们没有指定表空间， 那么分区将所属于缺省表空间。

如果对表进行了索引设置， 那么索引将创建在新分区上。 要使用ALTER TABLE... ADD PARTITION命令，我们必须是表的拥有者或有超级用户\(或管理员\)的权限。

## 参数 {#section_qg5_y9y_d04 .section}

|参数|参数说明|
|:-|:---|
|table name|要创建的表名称（可以采用模式限定的方式引用）。|
|partition name|要创建的分区名称。分区名称在所有分区和子分区中必须是唯一的，且必须遵循给对象标识符命名的惯例。|
|subpartition name|要创建的子分区名称。子分区名称在所有分区和子分区中必须是唯一的，且必须遵循给对象标识符命名的惯例。|
|\(value\[, value\]...\)|使用`value`来指定一个引用的文本值（或以逗号分隔的文本值列表）将表项目划分为不同的分区。每个分区规则必须至少指定一个值，但在规则中对于指定的值的数量没有上限要求。`Value`可能为`null`、`default` \(如果指定了一个`list`分区的话\) 或`maxvalue` \(如果指定了一个`range` 分区的话\)。 更多关于创建`default` 或`maxvalue`分区的信息请参见[在LIST 或 RANGE 分区表中处理偏离值](cn.zh-CN/POLARDB for Oracle开发指南/分区表使用/在LIST 或 RANGE 分区表中处理偏离值.md#)。

 |
|tablespace name|分区或子分区所属的表空间名称。|

## 示例 – 添加分区到LIST 分区表 {#section_k57_o02_3sl .section}

下列示例把分区添加到列表分区表sales中。通过使用下列命令创建表：

``` {#codeblock_4tx_joh_63r}
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

表包含三个分区\(americas, asia 和 europe\)：

``` {#codeblock_a9d_jfb_apo}
acctg=# SELECT partition_name, high_value FROM ALL_TAB_PARTITIONS;
 partition_name |     high_value      
----------------+---------------------
 americas       | 'US', 'CANADA'      
 asia           | 'INDIA', 'PAKISTAN' 
 europe         | 'FRANCE', 'ITALY'   
(3 rows)	
```

下述命令用于添加分区east\_asia到表sales中：

``` {#codeblock_71s_udw_hde}
ALTER TABLE sales ADD PARTITION east_asia 
  VALUES ('CHINA', 'KOREA');
```

在调用这个命令之后， 表包括了east\_asia分区。

``` {#codeblock_77m_amc_ap6}
acctg=# SELECT partition_name, high_value FROM ALL_TAB_PARTITIONS;
 partition_name |     high_value      
----------------+---------------------
 east_asia      | 'CHINA', 'KOREA'    
 americas       | 'US', 'CANADA'      
 asia           | 'INDIA', 'PAKISTAN' 
 europe         | 'FRANCE', 'ITALY'   
(4 rows)
```

## 示例 – 添加分区到RANGE 分区表 {#section_zg7_g94_il7 .section}

下列示例添加了一个分区到范围分区表sales中：

``` {#codeblock_ehf_2vg_oz4}
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

表包含四个分区\(q1\_2012, q2\_2012, q3\_2012 和 q4\_2012\)：

``` {#codeblock_5tr_06b_ak4}
acctg=# SELECT partition_name, high_value FROM ALL_TAB_PARTITIONS;
 partition_name |  high_value   
----------------+---------------
 q4_2012        | '2013-Jan-01' 
 q3_2012        | '2012-Oct-01' 
 q2_2012        | '2012-Jul-01' 
 q1_2012        | '2012-Apr-01' 
(4 rows)
```

下列命令添加了一个名为q1\_2013的分区到表sales 中：

``` {#codeblock_hik_47u_uuf}
ALTER TABLE sales ADD PARTITION q1_2013 
  VALUES LESS THAN('01-APR-2013');
```

在调用这个命令之后，表包括了分区q1\_2013：

``` {#codeblock_txl_wpe_b8t}
acctg=# SELECT partition_name, high_value FROM ALL_TAB_PARTITIONS;
 partition_name |  high_value   
----------------+---------------
 q1_2012        | '2012-Apr-01' 
 q2_2012        | '2012-Jul-01' 
 q3_2012        | '2012-Oct-01' 
 q4_2012        | '2013-Jan-01' 
 q1_2013        | '01-APR-2013' 
(5 rows)
```

