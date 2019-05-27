# statio\_indexes\_rpt\(\) {#concept_264534 .concept}

函数的签名如下：

``` {#codeblock_old_ndr_jty}
statio_indexes_rpt(beginning_id, ending_id, top_n, scope)
```

## 参数 {#section_m8e_8qg_htv .section}

|参数名称|描述|
|----|--|
|beginning\_id|beginning\_id是一个整数值，用于表示会话开始时的快照ID。|
|ending\_id|ending\_id是一个整数值，用于表示会话结束时的快照ID。|
|top\_n|top\_n表示由函数所返回记录的条数。|
|scope|参数scope决定了返回统计信息的范围（ALL, USER 或SYS）。 -   SYS 表示函数应返回与系统定义的表的相关信息。如果表存储于pg\_catalog、 information\_schema、 sys 或 dbo 模式中的任何一种模式中， 那么这个表就会被认作系统表。
-   USER 表示函数应该返回关于用户定义的表的信息。
-   ALL 指定函数应该返回关于所有表的信息。

 |

## 示例 {#section_9la_6bo_tyf .section}

下面的示例演示了对函数statio\_indexes\_rpt\(\)的调用以及函数的输出：

``` {#codeblock_t5q_izx_cyd}
edb=# SELECT * FROM statio_indexes_rpt(9, 10, 10, 'SYS');

                            statio_indexes_rpt
-----------------------------------------------------------------------------
   DATA from pg_statio_all_indexes

 SCHEMA      RELATION        INDEX
                        IDX BLKS READ   IDX BLKS HIT    IDX BLKS ICACHE HIT
-----------------------------------------------------------------------------
public               pgbench_accounts          pgbench_accounts_pkey
                        59              32126           9
 sys                  edb$stat_all_indexes      edb$stat_idx_pk
                        4               233             0
 sys                  edb$statio_all_indexes    edb$statio_idx_pk
                        4               233             0
 sys                  edb$stat_all_tables       edb$stat_tab_pk
                        2               174             0
 sys                  edb$statio_all_tables     edb$statio_tab_pk
                        2               174             0
 sys                  edb$session_wait_history  session_waits_hist_pk
                        4               47              0
 pg_catalog           pg_cast                   pg_cast_source_target_index
                        1               29              0
 pg_catalog           pg_trigger                pg_trig_tgrelid_tgname_index
                        1               15              0
 pg_catalog           pg_class                  pg_class_oid_index
                        1               14              0
 pg_catalog           pg_statistic              pg_statistic_relid_att_index
                        2               12              0
(14 rows)
```

DATA from pg\_statio\_all\_indexes中显示的信息包括：

|Column Name|Description|
|-----------|-----------|
|SCHEMA|The name of the schema in which the relation resides.|
|RELATION|The name of the table on which the index is defined.|
|INDEX|The name of the index.|
|IDX BLKS READ|The number of index blocks read.|
|IDX BLKS HIT|The number of index blocks hit.|
|IDX BLKS ICACHE HIT|The number of index blocks in Infinite Cache that were hit.|

