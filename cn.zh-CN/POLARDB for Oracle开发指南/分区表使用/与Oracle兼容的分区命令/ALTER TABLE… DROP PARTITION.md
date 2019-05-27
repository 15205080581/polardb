# ALTER TABLE… DROP PARTITION {#concept_222001 .concept}

## 语法介绍 {#section_rv4_1xl_zza .section}

使用ALTER TABLE. DROP PARTITION命令来删除分区定义和这个分区中的数据。语法如下：

``` {#codeblock_ew5_yr9_er3}
ALTER TABLE table_name DROP PARTITION partition_name;
```

## 描述 {#section_0bv_vxw_cnd .section}

ALTER TABLE, DROP PARTITION命令用于删除分区和存储在这个分区上的数据。当我们删除一个分区时，这个分区的任何子分区也会被删除。

要使用DROP PARTITION子句，我们必须是分区根的拥有者、拥有表的小组的成员或拥有数据库超级用户或管理员的权限。

## 参数 {#section_d8u_7qt_ym8 .section}

|参数|参数说明|
|:-|:---|
|table name|分区表名称（可以采用模式限定的方式引用）。|
|partition name|要删除的分区名称|

## 示例 – 删除分区 {#section_fqw_kzf_1su .section}

下列示例删除了表 sales的一个分区。通过使用下列命令来创建表 sales：

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

查询视图ALL\_TAB\_PARTITIONS 显示分区名称：

```
acctg=# SELECT partition_name, server_name, high_value FROM ALL_TAB_PARTITIONS;
 partition_name | server_name |     high_value      
----------------+-------------+---------------------
 europe         | seattle     | 'FRANCE', 'ITALY'
 asia           | chicago     | 'INDIA', 'PAKISTAN'
 americas       | boston      | 'US', 'CANADA'
(3 rows)
```

要从表 sales中删除分区americas，要先调用下列命令：

``` {#codeblock_cci_hqb_myf}
ALTER TABLE sales DROP PARTITION americas;
```

查询视图 ALL\_TAB\_PARTITIONS 显示了分区已被成功删除：

```
acctg=# SELECT partition_name, server_name, high_value FROM ALL_TAB_PARTITIONS;
 partition_name |     high_value      
----------------+---------------------
 asia           | 'INDIA', 'PAKISTAN'
 europe         | 'FRANCE', 'ITALY'
(2 rows)
```

