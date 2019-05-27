# edbreport\(\) {#concept_264275 .concept}

函数edbreport\(\)包含来自其它报表函数中的数据，另外还有其它一些系统信息。函数签名是：

``` {#codeblock_2ct_1ub_dru}
edbreport(beginning_id, ending_id)
```

## 参数 {#section_nbs_7km_s4y .section}

|参数名称|描述|
|----|--|
|beginning id|beginning\_id是一个整数值，用于表示会话开始时的快照ID。|
|ending\_id|ending\_id 是一个整数值，用于表示会话结束时的快照ID。|

## 示例 {#section_6if_x9z_9ee .section}

下面的代码示例演示了对函数edbreport\(\)的调用：

``` {#codeblock_by7_mwl_ihu}
edb=# SELECT * FROM edbreport(9, 10);
                                                                       edbreport
-----------------------------------------------------------------------------
    EnterpriseDB Report for database edb        23-AUG-15
 Version: EnterpriseDB 9.5.0.0 on i686-pc-linux-gnu
      Begin snapshot: 9 at 23-AUG-15 13:45:07.165123
      End snapshot:   10 at 23-AUG-15 13:45:35.653036

 Size of database edb is 155 MB
      Tablespace: pg_default Size: 179 MB Owner: enterprisedb
      Tablespace: pg_global  Size: 435 kB Owner: enterprisedb

 Schema: pg_toast_temp_1         Size: 0 bytes    Owner: enterprisedb
 Schema: public                  Size: 0 bytes    Owner: enterprisedb
 Schema: enterprisedb            Size: 143 MB     Owner: enterprisedb
 Schema: pgagent                 Size: 192 kB     Owner: enterprisedb
 Schema: dbms_job_procedure      Size: 0 bytes    Owner: enterprisedb
			
```

报告介绍中显示的信息包括数据库名称和版本、当前日期、开始和结束快照日期和时间、数据库和表空间细节以及模式信息。

``` {#codeblock_lue_s0a_979}
                Top 10 Relations by pages

 TABLE                                        RELPAGES
 ----------------------------------------------------------------------------
 pgbench_accounts                              15874
 pg_proc                                       102
 edb$statio_all_indexes                        73
 edb$stat_all_indexes                          73
 pg_attribute                                  67
 pg_depend                                     58
 edb$statio_all_tables                         49
 edb$stat_all_tables                           47
 pgbench_tellers                               37
 pg_description                                32
```

Top 10 Relations by pages显示信息包括：

|Column Name|Description|
|-----------|-----------|
|TABLE|The name of the table.|
|RELPAGES|The number of pages in the table.|

``` {#codeblock_2s5_eeh_sg4}
                Top 10 Indexes by pages

 INDEX                                        RELPAGES
 ----------------------------------------------------------------------------
 pgbench_accounts_pkey                         2198
 pg_depend_depender_index                      32
 pg_depend_reference_index                     31
 pg_proc_proname_args_nsp_index                30
 pg_attribute_relid_attnam_index               23
 pg_attribute_relid_attnum_index               17
 pg_description_o_c_o_index                    15
 edb$statio_idx_pk                             11
 edb$stat_idx_pk                               11
 pg_proc_oid_index                             9
```

Top 10 Indexes by pages显示信息包括：

|Column Name|Description|
|-----------|-----------|
|INDEX|The name of the index.|
|RELPAGES|The number of pages in the index.|

``` {#codeblock_iax_h5m_ytu}
                 Top 10 Relations by DML

 SCHEMA          RELATION                       UPDATES   DELETES   INSERTS
 ---------------------------------------------------------------------------
 enterprisedb    pgbench_accounts               10400     0         1000000
 enterprisedb    pgbench_tellers                10400     0         100
 enterprisedb    pgbench_branches               10400     0         10
 enterprisedb    pgbench_history                0         0         10400
 pgagent         pga_jobclass                   0         0         6
 pgagent         pga_exception                  0         0         0
 pgagent         pga_job                        0         0         0
 pgagent         pga_jobagent                   0         0         0
 pgagent         pga_joblog                     0         0         0
 pgagent         pga_jobstep                    0         0         0
```

Top 10 Relations by DML显示信息包括：

|Column Name|Description|
|-----------|-----------|
|SCHEMA|The name of the schema in which the table resides.|
|RELATION|The name of the table.|
|UPDATES|The number of UPDATES performed on the table.|
|DELETES|The number of DELETES performed on the table.|
|INSERTS|The number of INSERTS performed on the table.|

``` {#codeblock_xuz_r3x_6bj}
   DATA from pg_stat_database

 DATABASE   NUMBACKENDS  XACT COMMIT  XACT ROLLBACK   BLKS READ  BLKS HIT   BLKS ICACHE HIT      HIT RATIO  ICACHE HIT RATIO
 ----------------------------------------------------------------------------
 edb        0            142          0               78         10446
    0                 99.26      0.00
   DATA from pg_buffercache not included because pg_buffercache is not installed
```

DATA from pg\_stat\_database显示信息包括：

|Column Name|Description|
|-----------|-----------|
|DATABASE|The name of the database.|
|NUMBACKENDS|Number of backends currently connected to this database. This is the only column in this view that returns a value reflecting current state; all other columns return the accumulated values since the last reset.|
|XACT COMMIT|Number of transactions in this database that have been committed.|
|XACT ROLLBACK|Number of transactions in this database that have been rolled back.|
|BLKS READ|Number of disk blocks read in this database.|
|BLKS HIT|Number of times disk blocks were found already in the buffer cache \(when a read was not necessary\).|
|BLKS ICACHE HIT|The number of blocks found in Infinite Cache.|
|HIT RATIO|The percentage of times that a block was found in the shared buffer cache.|
|ICACHE HIT RATIO|The percentage of times that a block was found in Infinite Cache.|

``` {#codeblock_win_pk8_ali}
   DATA from pg_stat_all_tables ordered by seq scan

 SCHEMA               RELATION                       SEQ SCAN   REL TUP READ IDX SCAN   IDX TUP READ INS    UPD    DEL
 ----------------------------------------------------------------------------
 pg_catalog           pg_class                       16         7162         546        319          0      1      0
 pg_catalog           pg_am                          13         13           0          0            0      0      0
 pg_catalog           pg_database                    4          16           42         42           0      0      0
 pg_catalog           pg_index                       4          660          145        149          0      0      0
 pg_catalog           pg_namespace                   4          100          49         49           0      0      0
 sys                  edb$snap                       1          9            0          0            1      0      0
 pg_catalog           pg_authid                      1          1            25         25           0      0      0
 sys                  edb$session_wait_history       0          0            0          0            50     0      0
 sys                  edb$session_waits              0          0            0          0            2      0      0
 sys                  edb$stat_all_indexes           0          0            0          0            165    0      0
```

DATA from pg\_stat\_all\_tables ordered by seq scan显示信息包括：

|Column Name|Description|
|-----------|-----------|
|SCHEMA|The name of the schema in which the table resides.|
|RELATION|The name of the table.|
|SEQ SCAN|The number of sequential scans initiated on this table..|
|REL TUP READ|The number of tuples read in the table.|
|IDX SCAN|The number of index scans initiated on the table.|
|IDX TUP READ|The number of index tuples read.|
|INS|The number of rows inserted.|
|UPD|The number of rows updated.|
|DEL|The number of rows deleted.|

``` {#codeblock_2yy_tl3_j45}
   DATA from pg_stat_all_tables ordered by rel tup read

 SCHEMA               RELATION                       SEQ SCAN   REL TUP READ IDX SCAN   IDX TUP READ INS    UPD    DEL
 ----------------------------------------------------------------------------
 pg_catalog           pg_class                       16         7162         546        319          0      1      0
 pg_catalog           pg_index                       4          660          145        149          0      0      0
 pg_catalog           pg_namespace                   4          100          49         49           0      0      0
 pg_catalog           pg_database                    4          16           42         42           0      0      0
 pg_catalog           pg_am                          13         13           0          0            0      0      0
 sys                  edb$snap                       1          9            0          0            1      0      0
 pg_catalog           pg_authid                      1          1            25         25           0      0      0
 sys                  edb$session_wait_history       0          0            0          0            50     0      0
 sys                  edb$session_waits              0          0            0          0            2      0      0
 sys                  edb$stat_all_indexes           0          0            0          0            165    0      0
```

DATA from pg\_stat\_all\_tables ordered by rel tup read显示信息包括：

|Column Name|Description|
|-----------|-----------|
|SCHEMA|The name of the schema in which the table resides.|
|RELATION|The name of the table.|
|SEQ SCAN|The number of sequential scans performed on the table.|
|REL TUP READ|The number of tuples read from the table.|
|IDX SCAN|The number of index scans performed on the table.|
|IDX TUP READ|The number of index tuples read.|
|INS|The number of rows inserted.|
|UPD|The number of rows updated.|
|DEL|The number of rows deleted.|

``` {#codeblock_99u_68d_dta}
   DATA from pg_statio_all_tables

 SCHEMA      RELATION             HEAP     HEAP     HEAP     IDX      IDX
                                  READ     HIT      ICACHE   READ     HIT
                                                    HIT

             IDX      TOAST    TOAST    TOAST    TIDX     TIDX    TIDX
             ICACHE   READ     HIT      ICACHE   READ     HIT     ICACHE
             HIT                        HIT                       HIT
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
```

DATA from pg\_statio\_all\_tables显示信息包括：

|Column Name|Description|
|-----------|-----------|
|SCHEMA|The name of the schema in which the table resides.|
|RELATION|The name of the table.|
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

``` {#codeblock_x77_gv8_dit}
   DATA from pg_stat_all_indexes

 SCHEMA               RELATION                  INDEX                        IDX SCAN   IDX TUP READ IDX TUP FETCH
 ----------------------------------------------------------------------------
 pg_catalog           pg_attribute              pg_attribute_relid_attnum_index     427        907          907
 pg_catalog           pg_class                  pg_class_relname_nsp_index    289        62           62
 pg_catalog           pg_class                  pg_class_oid_index           257        257          257
 pg_catalog           pg_statistic              pg_statistic_relid_att_inh_index    207        196          196
 enterprisedb         pgbench_accounts          pgbench_accounts_pkey        200        255          200
 pg_catalog           pg_cast                   pg_cast_source_target_index  199        50           50
 pg_catalog           pg_proc                   pg_proc_oid_index            116        116          116
 pg_catalog           edb_partition             edb_partition_partrelid_index 112        0            0
 pg_catalog           edb_policy                edb_policy_object_name_index 112        0            0
 enterprisedb         pgbench_branches          pgbench_branches_pkey        101        110          0
```

DATA from pg\_stat\_all\_indexes显示信息包括：

|Column Name|Description|
|-----------|-----------|
|SCHEMA|The name of the schema in which the index resides.|
|RELATION|The name of the table on which the index is defined.|
|INDEX|The name of the index.|
|IDX SCAN|The number of indexes scans initiated on this index.|
|IDX TUP READ|Number of index entries returned by scans on this index.|
|IDX TUP FETCH|Number of live table rows fetched by simple index scans using this index.|

``` {#codeblock_wy5_od3_pvf}
   DATA from pg_statio_all_indexes

 SCHEMA               RELATION                  INDEX                               IDX BLKS READ   IDX BLKS HIT    IDX BLKS ICACHE HIT
 ----------------------------------------------------------------------------
 pg_catalog           pg_attribute              pg_attribute_relid_attnum_index     0               867             0
 enterprisedb         pgbench_accounts          pgbench_accounts_pkey               1               778             0
 pg_catalog           pg_class                  pg_class_relname_nsp_index          0               590             0
 pg_catalog           pg_class                  pg_class_oid_index                  0               527             0
 pg_catalog           pg_statistic              pg_statistic_relid_att_inh_index    0               441             0
 sys                  edb$stat_all_indexes      edb$stat_idx_pk                     1               332             0
 sys                  edb$statio_all_indexes    edb$statio_idx_pk                   1               332             0
 pg_catalog           pg_proc                   pg_proc_oid_index                   0               244             0
 sys                  edb$stat_all_tables       edb$stat_tab_pk                     0               241             0
 sys                  edb$statio_all_tables     edb$statio_tab_pk                   0               241             0
```

DATA from pg\_statio\_all\_indexes显示信息包括：

|Column Name|Description|
|-----------|-----------|
|SCHEMA|The name of the schema in which the index resides.|
|RELATION|The name of the table on which the index is defined.|
|INDEX|The name of the index.|
|IDX BLKS READ|The number of index blocks read.|
|IDX BLKS HIT|The number of index blocks hit.|
|IDX BLKS ICACHE HIT|The number of index blocks in Infinite Cache that were hit.|

``` {#codeblock_yog_11u_36a}
    System Wait Information

 WAIT NAME                                COUNT      WAIT TIME       % WAIT
 ---------------------------------------------------------------------------
 query plan                               0          0.000407        100.00
 db file read                             0          0.000000        0.00
```

System Wait Information显示信息包括：

|Column Name|Description|
|-----------|-----------|
|WAIT NAME|The name of the wait.|
|COUNT|The number of times that the wait event occurred.|
|WAIT TIME|The length of the wait time in milliseconds.|
|% WAIT|The percentage of the total wait time used by this wait for this session.|

``` {#codeblock_ekj_ml5_lnb}
    Database Parameters from postgresql.conf

 PARAMETER                         SETTING                                  CONTEXT     MINVAL       MAXVAL
 ----------------------------------------------------------------------------
 allow_system_table_mods            off                                      postmaster
 application_name                   psql                                     user
 archive_command                    (disabled)                               sighup
 archive_mode                       off                                      postmaster
 archive_timeout                    0                                        sighup      0            2147483647
 array_nulls                        on                                       user
 authentication_timeout             60                                       sighup      1            600
 autovacuum                         on                                       sighup
 autovacuum_analyze_scale_factor    0.1                                      sighup      0            100
 autovacuum_analyze_threshold       50                                       sighup      0            2147483647
 autovacuum_freeze_max_age          200000000                                postmaster  100000000    2000000000
 autovacuum_max_workers             3                                        postmaster  1            8388607
 autovacuum_naptime                 60                                       sighup      1            2147483
 autovacuum_vacuum_cost_delay       20                                       ...
				
```

Database Parameters from postgresql.conf显示信息包括：

|Column Name|Description|
|-----------|-----------|
|PARAMETER|The name of the parameter.|
|SETTING|The current value assigned to the parameter.|
|CONTEXT|The context required to set the parameter value.|
|MINVAL|The minimum value allowed for the parameter.|
|MAXVAL|The maximum value allowed for the parameter.|

