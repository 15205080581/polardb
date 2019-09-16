# stat\_indexes\_rpt\(\) {#concept_264531 .concept}

函数的签名如下：

``` {#codeblock_prb_1nd_s63}
stat_indexes_rpt(beginning_id, ending_id, top_n, scope)
```

## 参数 {#section_4nu_nfo_ri8 .section}

|参数名称|描述|
|----|--|
|beginning\_id|beginning\_id是一个整数值，用于表示会话开始时的快照ID。|
|ending\_id|ending\_id是一个整数值，用于表示会话结束时的快照ID。|
|top\_n|top\_n表示由函数所返回记录的条数。|
|scope|参数scope决定了返回统计信息的范围（ALL, USER 或SYS）。 -   SYS 表示函数应返回与系统定义的表的相关信息。如果表存储于pg\_catalog、 information\_schema、 sys 或 dbo 模式中的任何一种模式中， 那么这个表就会被认作系统表。
-   USER 表示函数应该返回关于用户定义的表的信息。
-   ALL 指定函数应该返回关于所有表的信息。

 |

## 示例 {#section_kmk_cqs_cic .section}

下面的代码示例演示了对函数stat\_indexes\_rpt\(\)的调用，以及函数的输出结果：

``` {#codeblock_k2v_rlj_r5y}
edb=# SELECT * FROM stat_indexes_rpt(9, 10, 10, 'ALL');

                            stat_indexes_rpt
-----------------------------------------------------------------------------
   DATA from pg_stat_all_indexes

 SCHEMA        RELATION        INDEX
                          IDX SCAN    IDX TUP READ    IDX TUP FETCH
-----------------------------------------------------------------------------
 pg_catalog    pg_cast         pg_cast_source_target_index
                          30          7               7
 pg_catalog    pg_class        pg_class_oid_index
                          15          15              15
 pg_catalog    pg_trigger      pg_trigger_tgrelid_tgname_index
                          12          12              12
 pg_catalog    pg_attribute    pg_attribute_relid_attnum_index
                          7           31              31
 pg_catalog    pg_statistic    pg_statistic_relid_att_index
                          7           0               0
 pg_catalog    pg_database     pg_database_oid_index
                          5           5               5
 pg_catalog    pg_proc         pg_proc_oid_index
                          5           5               5
 pg_catalog    pg_operator     pg_operator_oprname_l_r_n_index
                          3           1               1
 pg_catalog    pg_type         pg_type_typname_nsp_index
                          3           1               1
 pg_catalog    pg_amop         pg_amop_opr_fam_index
                          2           3               3
(14 rows)
```

DATA from pg\_stat\_all\_indexes中显示的信息包括：

|Column Name|Description|
|-----------|-----------|
|SCHEMA|The name of the schema in which the relation resides.|
|RELATION|The name of the relation.|
|INDEX|The name of the index.|
|IDX SCAN|The number of indexes scanned.|
|IDX TUP READ|The number of index tuples read.|
|IDX TUP FETCH|The number of index tuples fetched.|

