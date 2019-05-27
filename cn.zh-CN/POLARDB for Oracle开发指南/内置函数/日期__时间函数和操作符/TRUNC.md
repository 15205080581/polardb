# TRUNC {#concept_221933 .concept}

函数TRUNC返回一个根据指定模板模式截断的日期类型值。如果没有使用模板模式，那么就把日期截断到离它最近的一天。下面的表格显示了函数TRUNC所允许使用的模板模式。

|Pattern|Description|
|-------|-----------|
|CC, SCC|Returns January 1, cc01 where cc is first 2 digits of the given year|
|SYYY, YYYY, YEAR, SYEAR, YYY, YY, Y|Returns January 1, yyyy where yyyy is the given year|
|IYYY, IYY, IY, I|Returns the start date of the ISO year containing the given date|
|Q|Returns the first day of the quarter containing the given date|
|MONTH, MON, MM, RM|Returns the first day of the specified month|
|WW|Returns the largest date just prior to, or the same as the given date that corresponds to the same day of the week as the first day of the year|
|IW|Returns the start of the ISO week containing the given date|
|W|Returns the largest date just prior to, or the same as the given date that corresponds to the same day of the week as the first day of the month|
|DDD, DD, J|Returns the start of the day for the given date|
|DAY, DY, D|Returns the start of the week \(Sunday\) containing the given date|
|HH, HH12, HH2 4|Returns the start of the hour|
|MI|Returns the start of the minute|

## TRUNC函数示例 {#section_vhk_zfp_rhr .section}

下面的示例把日期向前截断为日期所在世纪的开始日期。

``` {#codeblock_3gf_ivj_d0n}
SELECT TO_CHAR(TRUNC(TO_DATE('1951','YYYY'),'CC'),'DD-MON-YYYY') "Century" FROM DUAL;

   Century
-------------
 01-JAN-1901
(1 row)	
```

下面的示例把日期截断到日期中年份的开始日期。

``` {#codeblock_xht_ook_ig1}
SELECT TO_CHAR(TRUNC(TO_DATE('01-JUL-1999','DD-MON-YYYY'),'Y'),'DD-MON-YYYY') "Year" FROM DUAL;

    Year
-------------
 01-JAN-1999
(1 row)
```

下面的示例把日期截断到ISO年份的开始日期。

``` {#codeblock_g5y_ri5_f95}
SELECT TO_CHAR(TRUNC(TO_DATE('01-JUL-2004','DD-MON-YYYY'),'IYYY'),'DD-MON-YYYY') "ISO Year" FROM DUAL;

  ISO Year
-------------
 29-DEC-2003
(1 row)		
```

下面的示例把日期截断到当前日期所在季度的开始日期。

``` {#codeblock_on0_b8w_dq8}
SELECT TRUNC(TO_DATE('16-FEB-07','DD-MON-YY'),'Q') "Quarter" FROM DUAL;

      Quarter
--------------------
 01-JAN-07 00:00:00
(1 row)	
```

下面的示例把日期截断到一个月的开始日期。

``` {#codeblock_97l_mq2_pqd}
SELECT TRUNC(TO_DATE('16-DEC-07','DD-MON-YY'),'MONTH') "Month" FROM DUAL;

       Month
--------------------
 01-DEC-07 00:00:00
(1 row)
```

下面的示例把日期截断到日期所在周的开始日期，周的开始日期是由一年中第一天的周日期决定的。例如：2007年的第一天是周一，所以在1月19日前面的周一的日期是1月15号。

``` {#codeblock_hjf_v2v_dgh}
SELECT TRUNC(TO_DATE('19-JAN-07','DD-MON-YY'),'WW') "Week" FROM DUAL;

        Week
--------------------
 15-JAN-07 00:00:00
(1 row)
```

下面的示例将日期截断到一个ISO周的开始。一个ISO周在星期一开始，落在ISO周的日期是2004年1月2号，那么这个ISO周从2003年12月29日开始。

``` {#codeblock_s0e_pca_o61}
SELECT TRUNC(TO_DATE('02-JAN-04','DD-MON-YY'),'IW') "ISO Week" FROM DUAL;

      ISO Week
--------------------
 29-DEC-03 00:00:00
(1 row)
```

下面的示例把日期截断到一周的开始日期，周的开始日期被认为和一个月的第一天相同。

``` {#codeblock_xvm_sh5_rzm}
SELECT TRUNC(TO_DATE('21-MAR-07','DD-MON-YY'),'W') "Week" FROM DUAL;

        Week
--------------------
 15-MAR-07 00:00:00
(1 row)
```

下面的示例把日期截断到一天的开始时间。

``` {#codeblock_wiz_my2_ds9}
SELECT TRUNC(TO_DATE('04-AUG-07 12:00:00 PM','DD-MON-YY HH:MI:SS AM'),'J') "Day" FROM DUAL;

        Day
--------------------
 04-AUG-07 00:00:00
(1 row)
```

下面的示例把日期截断到一周的开始日期（周日）。

``` {#codeblock_0yf_ao0_wvs}
SELECT TRUNC(TO_DATE('09-AUG-07','DD-MON-YY'),'DAY') "Day of Week" FROM DUAL;

    Day of Week
--------------------
 05-AUG-07 00:00:00
(1 row)
```

下面的示例把日期截断到小时。

``` {#codeblock_nxf_8eb_kie}
SELECT TO_CHAR(TRUNC(TO_DATE('09-AUG-07 08:30','DD-MON-YY HH:MI'),'HH'),'DD-MON-YY HH24:MI:SS') "Hour" FROM DUAL;

        Hour
--------------------
 09-AUG-07 08:00:00
(1 row)
```

下面的示例把日期截断到分钟。

``` {#codeblock_xrk_idf_fht}
SELECT TO_CHAR(TRUNC(TO_DATE('09-AUG-07 08:30:30','DD-MON-YY HH:MI:SS'),'MI'),'DD-MON-YY HH24:MI:SS') "Minute" FROM DUAL;

       Minute
--------------------
 09-AUG-07 08:30:00
(1 row)
```

