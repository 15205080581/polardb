# stat\_tables\_rpt\(\) {#concept_264447 .concept}

函数的签名如下：

``` {#codeblock_6p5_5xu_lcn}
function_name(beginning_id, ending_id, top_n, scope)
```

## 参数 {#section_o3q_kh8_7jw .section}

|参数名称|描述|
|----|--|
|beginning\_id|beginning\_id是一个整数值，用于表示会话开始时的快照ID。|
|ending\_id|ending\_id是一个整数值，用于表示会话结束时的快照ID。|
|top\_n|top\_n表示由函数所返回记录的条数。|
|scope|参数scope决定了返回统计信息的范围（ALL, USER 或SYS）。 -   SYS 表示函数应返回与系统定义的表的相关信息。如果表存储于pg\_catalog、 information\_schema、 sys 或 dbo 模式中的任何一种模式中， 那么这个表就会被认作系统表。
-   USER 表示函数应该返回关于用户定义的表的信息。
-   ALL 指定函数应该返回关于所有表的信息。

 |

## 示例 {#section_uav_j3x_irp .section}

下面的代码演示了函数stat\_tables\_rpt\(\)及其函数的输出结果：

``` {#codeblock_en8_kkj_uke}
SELECT * FROM stat_tables_rpt(18, 19, 10, 'ALL');

stat_tables_rpt
-----------------------------------------------------------------------------
DATA from pg_stat_all_tables ordered by seq scan

SCHEMA        RELATION
    SEQ SCAN   REL TUP READ IDX SCAN   IDX TUP READ   INS    UPD    DEL
-----------------------------------------------------------------------------
pg_catalog    pg_class
    8          2952         78         65             0      0      0
pg_catalog    pg_index
    4          448          23         28             0      0      0
pg_catalog    pg_namespace
    4          76           1          1              0      0      0
pg_catalog    pg_database
    3          6            0          0              0      0      0
pg_catalog    pg_authid
    2          1            0          0              0      0      0
sys           edb$snap
    1          15           0          0              1      0      0
public        accounts
    0          0            0          0              0      0      0
public        branches
    0          0            0          0              0      0      0
sys           edb$session_wait_history
    0          0            0          0              25     0      0
sys           edb$session_waits
    0          0            0          0              10     0      0
```

DATA from pg\_stat\_all\_tables ordered by seq scan中显示的信息包括：

|Column Name|Description|
|-----------|-----------|
|SCHEMA|The name of the schema in which the table resides.|
|RELATION|The name of the table.|
|SEQ SCAN|The number of sequential scans on the table.|
|REL TUP READ|The number of tuples read from the table.|
|IDX SCAN|The number of index scans performed on the table.|
|IDX TUP READ|The number of index tuples read from the table.|
|INS|The number of rows inserted.|
|UPD|The number of rows updated.|
|DEL|The number of rows deleted.|

报告的第二部分包括：

``` {#codeblock_zdt_6o1_a3u}
DATA from pg_stat_all_tables ordered by rel tup read

SCHEMA       RELATION
    SEQ SCAN   REL TUP READ IDX SCAN   IDX TUP READ INS    UPD    DEL
-----------------------------------------------------------------------------
pg_catalog   pg_class
    8          2952         78         65           0      0      0
pg_catalog   pg_index
    4          448          23         28           0      0      0
pg_catalog   pg_namespace
    4          76           1          1            0      0      0
sys          edb$snap
    1          15           0          0            1      0      0
pg_catalog   pg_database
    3          6            0          0            0      0      0
pg_catalog   pg_authid
    2          1            0          0            0      0      0
public       accounts
    0          0            0          0            0      0      0
public       branches
    0          0            0          0            0      0      0
sys          edb$session_wait_history
    0          0            0          0            25     0      0
sys          edb$session_waits
    0          0            0          0            10     0      0
(29 rows)
```

DATA from pg\_stat\_all\_tables ordered by rel tup read中显示的信息包括：

|Column Name|Description|
|-----------|-----------|
|SCHEMA|The name of the schema in which the table resides.|
|RELATION|The name of the table.|
|SEQ SCAN|The number of sequential scans performed on the table.|
|REL TUP READ|The number of tuples read from the table.|
|IDX SCAN|The number of index scans performed on the table.|
|IDX TUP READ|The number of live rows fetched by index scans.|
|INS|The number of rows inserted.|
|UPD|The number of rows updated.|
|DEL|The number of rows deleted.|

