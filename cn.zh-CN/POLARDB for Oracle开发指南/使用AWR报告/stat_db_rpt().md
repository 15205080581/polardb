# stat\_db\_rpt\(\) {#concept_264438 .concept}

函数的签名如下：

``` {#codeblock_mw5_udg_3u9}
stat_db_rpt(beginning_id, ending_id)
```

## 参数 {#section_7gw_t4i_27k .section}

|参数名称|描述|
|----|--|
|beginning id|beginning\_id是一个整数值，用于表示会话开始时的快照ID。|
|ending id|ending\_id是一个整数值，用于表示会话结束时的快照ID。|

## 示例 {#section_z21_n9l_ogd .section}

下面的示例演示对函数stat\_db\_rpt\(\)的调用：

``` {#codeblock_ft8_xwz_ykm}
SELECT * FROM stat_db_rpt(9, 10);
                               stat_db_rpt
-----------------------------------------------------------------------------
   DATA from pg_stat_database

 DATABASE   NUMBACKENDS  XACT COMMIT  XACT ROLLBACK   BLKS READ  BLKS HIT
        BLKS ICACHE HIT      HIT RATIO      ICACHE HIT RATIO
-----------------------------------------------------------------------------
 edb        1            21           0               92928      101217
        301                  52.05          0.15
```

DATA from pg\_stat\_database中显示的信息包括：

|Column Name|Description|
|-----------|-----------|
|DATABASE|The name of the database.|
|NUMBACKENDS|Number of backends currently connected to this database. This is the only column in this view that returns a value reflecting current state; all other columns return the accumulated values since the last reset.|
|XACT COMMIT|The number of transactions in this database that have been committed.|
|XACT ROLLBACK|The number of transactions in this database that have been rolled back.|
|BLKS READ|The number of blocks read.|
|BLKS HIT|The number of blocks hit.|
|BLKS ICACHE HIT|The number of blocks in Infinite Cache that were hit.|
|HIT RATIO|The percentage of times that a block was found in the shared buffer cache.|
|ICACHE HIT RATIO| |

