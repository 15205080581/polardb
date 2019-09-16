# statio\_tables\_rpt\(\) {#concept_264521 .concept}

函数的签名如下：

``` {#codeblock_xbq_i9i_3im}
statio_tables_rpt(beginning_id, ending_id, top_n, scope)
```

## 参数 {#section_wuu_8b5_9zr .section}

|参数名称|描述|
|----|--|
|beginning\_id|beginning\_id是一个整数值，用于表示会话开始时的快照ID。|
|ending\_id|ending\_id是一个整数值，用于表示会话结束时的快照ID。|
|top\_n|top\_n表示由函数所返回记录的条数。|
|scope|参数scope决定了返回统计信息的范围（包括ALL, USER 或SYS）。 -   SYS 表示函数应返回与系统定义的表的相关信息。如果表存储于pg\_catalog、 information\_schema、 sys 或 dbo 模式中的任何一种模式中， 那么这个表就会被认作系统表。
-   USER 表示函数应该返回关于用户定义的表的信息。
-   ALL 指定函数应该返回关于所有表的信息。

 |

## 示例 {#section_4tt_025_7nz .section}

下面的示例演示了对函数statio\_tables\_rpt\(\)的调用，及其函数的输出结果：

``` {#codeblock_tdm_sjp_4vr}
edb=# SELECT * FROM statio_tables_rpt(9, 10, 10, 'SYS');

                               statio_tables_rpt                                     
-----------------------------------------------------------------------------
   DATA from pg_statio_all_tables

 SCHEMA      RELATION             HEAP     HEAP     HEAP     IDX      IDX
                                  READ     HIT      ICACHE   READ     HIT
                                                    HIT

             IDX      TOAST    TOAST    TOAST    TIDX     TIDX    TIDX
             ICACHE   READ     HIT      ICACHE   READ     HIT     ICACHE
             HIT                      HIT                        HIT
-----------------------------------------------------------------------------
 public      pgbench_accounts     92766    67215    288      59       32126
             9        0        0        0        0        0        0
 pg_catalog  pg_class             0        296      0        3        16
             0        0        0        0        0        0        0
 sys         edb$stat_all_indexes 8        125      0        4        233
             0        0        0        0        0        0        0
 sys         edb$statio_all_index 8        125      0        4        233
             0        0        0        0        0        0        0
 sys         edb$stat_all_tables  6        91       0        2        174
             0        0        0        0        0        0        0
 sys         edb$statio_all_table 6        91       0        2        174
             0        0        0        0        0        0        0
 pg_catalog  pg_namespace         3        72       0        0        0
             0        0        0        0        0        0        0
 sys         edb$session_wait_his 1        24       0        4        47
             0        0        0        0        0        0        0
 pg_catalog  pg_opclass           3        13       0        2        0
             0        0        0        0        0        0        0
 pg_catalog  pg_trigger           0        12       0        1        15
             0        0        0        0        0        0        0
(16 rows)
```

Data from pg\_statio\_all\_tables中显示的信息包括：

|Column Name|Description|
|-----------|-----------|
|SCHEMA|The name of the schema in which the relation resides.|
|RELATION|The name of the relation.|
|HEAP READ|The number of heap blocks read.|
|HEAP HIT|The number of heap blocks hit.|
|HEAP ICACHE HIT|The number of heap blocks in Infinite Cache.|
|IDX READ|The number of index blocks read.|
|IDX HIT|The number of index blocks hit.|
|IDX ICACHE HIT|The number of index blocks in Infinite Cache.|
|TOAST READ|The number of toast blocks read.|
|TOAST HIT|The number of toast blocks hit.|
|TOAST ICACHE HIT|The number of toast blocks in Infinite Cache.|
|TIDX READ|The number of toast index blocks read.|
|TIDX HIT|The number of toast index blocks hit.|
|TIDX ICACHE HIT|The number of toast index blocks in Infinite Cache.|

