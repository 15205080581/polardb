# CURRENT DATE/TIME {#concept_221942 .concept}

POLARDB for Oracle提供了很多函数，用于返回与当前日期和时间相关的值。所有这些函数的返回值都是基于当前事务的开始时间。

-   CURRENT\_DATE
-   CURRENT\_TIMESTAMP
-   LOCALTIMESTAMP
-   LOCALTIMESTAMP\(precision\)

CURRENT\_DATE返回的是基于当前事务起始时间的当前日期和时间。如果在一个事务中同时调用多个时间，那么CURRENT\_DATE值将不会发生改变。

``` {#codeblock_nwe_kdg_fo7}
SELECT CURRENT_DATE FROM DUAL;

   date
-----------
 06-AUG-07    
```

CURRENT\_TIMESTAMP返回的是当前日期和时间。当从一个SQL语句中调用时，它将返回SQL语句中每次出现的相同值。如果在一个事务中同时调用多个语句，那么可能返回每次出现的不同值。如果在函数中调用语句，那么它可能返回不同的值，而不是在调用中由当前时间截返回的单一值。

``` {#codeblock_vta_du7_acc}
SELECT CURRENT_TIMESTAMP, CURRENT_TIMESTAMP FROM DUAL;

                current_timestamp | current_timestamp 
----------------------------------+----------------------------------
 02-SEP-13 17:52:29.261473 +05:00 | 02-SEP-13 17:52:29.261474 +05:00 
```

可以选择性地给予LOCALTIMESTAMP一个精确参数，且这个精确参数可以使结果四舍五入到秒字段的小数。如果不指定精确参数，那么结果为可得到的完整精度。

``` {#codeblock_lw6_zpb_mdw}
SELECT LOCALTIMESTAMP FROM DUAL;

       timestamp
------------------------
 06-AUG-07 16:11:35.973
(1 row)

SELECT LOCALTIMESTAMP(2) FROM DUAL;

       timestamp
-----------------------
 06-AUG-07 16:11:44.58
(1 row)
```

这些函数返回当前事务的开始时间，但是它们的值在事务运行期间不改变。这是一个值得考虑的特性：它的目的是允许单个事务有一致的当前时间，所以在同一事务中进行多个修改操作使用相同时间戳。其他数据库系统可以更频繁的使用这些值。

