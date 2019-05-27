# ALTER TABLE… RENAME PARTITION {#concept_221994 .concept}

## 语法介绍 {#section_251_3en_2li .section}

使用ALTER TABLE, RENAME PARTITION命令重命名表分区。ALTER TABLE, RENAME PARTITION命令有两种形式。

-   ```
ALTER TABLE table_name 
RENAME PARTITION partition_name 
TO new_name;
```

-   ```
ALTER TABLE table_name 
RENAME SUBPARTITION subpartition_name 
 TO new_name;
```


ALTER TABLE, RENAME PARTITION命令在分区和子分区之间没有任何区别。

-   我们可以使用 RENAME PARTITION 或 RENAME SUBPARTITION 子句来重命名分区。
-   我们可以使用RENAME PARTITION 或 RENAME SUBPARTITION 子句来重命名子分区。

## 描述 {#section_bd1_l5n_isr .section}

ALTER TABLE. RENAME PARTITION 和 ALTER TABLE. RENAME SUBPARTITION 命令用于重命名分区或子分区。我们必须拥有指定的表才能调用ALTER TABLE. RENAME PARTITION 或 ALTER TABLE. RENAME SUBPARTITION。

## 参数 {#section_ys3_d7r_tpb .section}

|参数|参数说明|
|:-|:---|
|target table|分区所属的表名称（可以采用模式限定的方式引用）。|
|partition name|要重命名的分区或子分区。|
|new name|分区或子分区的新名称。|

## 示例 – 重命名分区 {#section_wjm_p84_mmo .section}

下列命令创建了一个名为sales的列表分区表：

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

查询视图ALL\_TAB\_PARTITIONS来显示分区名称：

```
acctg=# SELECT partition_name, high_value FROM ALL_TAB_PARTITIONS;
 partition_name |     high_value      
----------------+---------------------
 europe         | 'FRANCE', 'ITALY'
 asia           | 'INDIA', 'PAKISTAN'
 americas       | 'US', 'CANADA'
(3 rows)
```

下列命令将分区americas重命名为n\_america：

```
ALTER TABLE sales 
RENAME PARTITION americas TO n_america;
```

查询视图ALL\_TAB\_PARTITIONS显示了已成功对分区进行了重命名：

```
acctg=# SELECT partition_name, high_value FROM ALL_TAB_PARTITIONS;
 partition_name |     high_value      
----------------+---------------------
 europe         | 'FRANCE', 'ITALY'
 asia           | 'INDIA', 'PAKISTAN'
 n_america      | 'US', 'CANADA'
(3 rows)
```

