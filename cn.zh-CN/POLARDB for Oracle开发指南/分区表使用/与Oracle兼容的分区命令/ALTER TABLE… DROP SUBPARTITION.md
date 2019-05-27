# ALTER TABLE… DROP SUBPARTITION {#concept_222002 .concept}

## 语法介绍 {#section_flo_bdd_xrn .section}

使用ALTER TABLE. DROP SUBPARTITION 命令来删除子分区定义及子分区内的数据。语法如下：

``` {#codeblock_r8z_u4o_6ct}
ALTER TABLE table_name DROP SUBPARTITION subpartition_name;
```

## 描述 {#section_sah_mq5_8sg .section}

ALTER TABLE, DROP SUBPARTITION 命令用于删除子分区及存储在子分区内的数据。 要使用DROP SUBPARTITION 子句，我们必须是分区根的拥有者、拥有表的小组成员或有超级用户或管理员的权限。

## 参数 {#section_jgz_9d9_qci .section}

|参数|参数说明|
|:-|:---|
|table name|分区表的名称（可以采用模式限定的方式引用\)。|
|subpartition name|要删除的子分区名称。|

## 示例 – 删除子分区 {#section_w52_vr5_ys0 .section}

下列示例删除了表sales中的一个子分区。通过使用下列命令来创建表sales：

```
CREATE TABLE sales
(
  dept_no     number,
  part_no     varchar2,
  country     varchar2(20),
  date    date,
  amount  number
)
PARTITION BY RANGE(date)
  SUBPARTITION BY LIST (country)
  (
    PARTITION first_half_2012 VALUES LESS THAN('01-JUL-2012')
    (
      SUBPARTITION europe VALUES ('ITALY', 'FRANCE'),
      SUBPARTITION americas VALUES ('CANADA', 'US'),
      SUBPARTITION asia VALUES ('PAKISTAN', 'INDIA')
    ),
    PARTITION second_half_2012 VALUES LESS THAN('01-JAN-2013') 
  );
```

查询视图ALL\_TAB\_SUBPARTITIONS 显示了子分区的名称：

```
acctg=# SELECT subpartition_name, high_value, server_name FROM ALL_TAB_SUBPARTITIONS; subpartition_name |     high_value      | server_name 
-------------------+---------------------+-------------
 europe            | 'ITALY', 'FRANCE'   | chicago
 americas          | 'CANADA', 'US'      | seattle
 asia              | 'PAKISTAN', 'INDIA' | boston
(3 rows)
```

要从表sales中删除子分区americas，就要先调用下列命令：

``` {#codeblock_ulo_1mq_ts9}
ALTER TABLE sales DROP SUBPARTITION americas;
```

查询视图ALL\_TAB\_SUBPARTITIONS显示了子分区已被成功删除：

```
acctg=# SELECT subpartition_name, high_value FROM ALL_TAB_SUBPARTITIONS;
 subpartition_name |     high_value      
-------------------+---------------------
 europe            | 'ITALY', 'FRANCE'
 asia              | 'PAKISTAN', 'INDIA'
(2 rows)
```

