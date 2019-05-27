# ALTER TABLE… MOVE PARTITION {#concept_221965 .concept}

## 语法介绍 {#section_n9j_nx7_gno .section}

使用ALTER TABLE. MOVE PARTITION命令将分区或子分区移动到不同的表空间中。ALTER TABLE. MOVE PARTITION命令有两种形式：

-   第一种形式是将分区移动到一个新的表空间中：

    ```
    ALTER TABLE table_name 
      MOVE PARTITION partition_name 
       TABLESPACE tablespace_name;
    ```

-   第二种形式是将子分区移动到一个新的表空间中：

    ```
    ALTER TABLE table_name 
      MOVE SUBPARTITION subpartition_name 
       TABLESPACE tablespace_name;
    ```


ALTER TABLE. MOVE PARTITION命令的语法在分区和子分区之间没有任何区别。

-   我们可以使用MOVE PARTITION 或 MOVE SUBPARTITION子句来移动分区。
-   我们可以使用MOVE PARTITION 或 MOVE SUBPARTITION子句来移动子分区。

## 描述 {#section_76s_kp2_0dy .section}

ALTER TABLE.MOVE PARTITION命令用于从分区或子分区当前的表空间中将其移动到不同的表空间。我们必须先拥有一个表，才能调用ALTER TABLE. MOVE PARTITION 或 ALTER TABLE. MOVE SUBPARTITION。

## 参数 {#section_h0x_7sn_d7k .section}

|参数|参数说明|
|:-|:---|
|target table|分区所属的表名称（可以采用模式限定的方式引用）。|
|partition name|要移动的分区或子分区的名称。|
|tablespace name|分区或子分区将要移动到的表空间名称。|

## 示例 – 将分区移动到不同的表空间中 {#section_2zc_zb7_wwk .section}

下列示例将表sales的分区从一个表空间移动到另一个表空间。首先，我们要使用这个命令创建表sales：

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
(
  PARTITION q1_2012 VALUES LESS THAN ('2012-Apr-01'),
  PARTITION q2_2012 VALUES LESS THAN ('2012-Jul-01'),
  PARTITION q3_2012 VALUES LESS THAN ('2012-Oct-01'),
  PARTITION q4_2012 VALUES LESS THAN ('2013-Jan-01') TABLESPACE ts_1,
  PARTITION q1_2013 VALUES LESS THAN ('2013-Mar-01') TABLESPACE ts_2
);
```

对视图ALL\_TAB\_PARTITIONS的查询确认了分区是否存储在既定的服务器之上和表空间之中：

```
acctg=# SELECT partition_name, tablespace_name FROM ALL_TAB_PARTITIONS;
 partition_name | tablespace_name 
----------------+-------------+-----------------
 q1_2013        | ts_2
 q4_2012        | ts_1
 q3_2012        | 
 q2_2012        | 
 q1_2012        | 
(5 rows)
```

在准备目标表空间之后，我们就可以通过调用ALTER TABLE. .. MOVE PARTITION命令从表空间ts\_2中将分区q1\_2013移动到表空间ts\_3中：

``` {#codeblock_cis_65y_vde}
ALTER TABLE sales MOVE PARTITION q1_2013 TABLESPACE ts_3; 
```

对视图ALL\_TAB\_PARTITIONS的查询显示了已成功执行移动操作：

```
acctg=# SELECT partition_name, tablespace_name FROM ALL_TAB_PARTITIONS;
 partition_name | tablespace_name 
----------------+-----------------
 q1_2013        | ts_3
 q4_2012        | ts_1
 q3_2012        | 
 q2_2012        | 
 q1_2012        | 
(5 rows)
```

