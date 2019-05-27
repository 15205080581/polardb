# DROP TABLE {#concept_221998 .concept}

## 语法介绍 {#section_0hi_g0p_9b7 .section}

使用PostgreSQL DROP TABLE命令来删除分区表定义及它的分区和子分区，并删除表内容。语法如下：

``` {#codeblock_d2v_yhj_g13}
DROP TABLE table_name
```

## 描述 {#section_9ou_xgn_e9g .section}

DROP TABLE命令用于删除整个表及表内的所有数据。当我们删除一个表时，这个表的所有分区或子分区也会被删除。

要使用DROP TABLE命令，我们必须是分区根的拥有者、拥有表的小组中的成员、模式拥有者或是数据库的超级用户。

## 参数 {#section_k55_4cw_6hk .section}

|参数|参数说明|
|:-|:---|
|table name|分区表名称（可以采用模式限定的方式引用）。|

## 示例 {#section_f64_ttv_p3d .section}

要删除表，就要先连接到控制器节点（分区根的主机）然后再调用DROP TABLE命令。例如，要删除表sales，就要调用下列命令：

``` {#codeblock_1bm_752_csh}
DROP TABLE sales;
```

服务器会确认表是否已被删除：

``` {#codeblock_l8s_uhx_70h}
acctg=# drop table sales;
DROP TABLE
acctg=#		
```

更多关于DROP TABLE命令的信息，请参见[PostgreSQL核心文件](http://www.enterprisedb.com/docs/en/9.3/pg/sql-droptable.html)。

