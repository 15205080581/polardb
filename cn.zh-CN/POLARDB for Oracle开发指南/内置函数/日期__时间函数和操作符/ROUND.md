# ROUND {#concept_221799 .concept}

函数ROUND根据指定的模板模式返回一个经过取整的日期类型值。如果没有指定模板模式，那么就把日期取整到最近的一天。下面的表显示了函数ROUND所使用的模板模式。

|Pattern|Description|
|-------|-----------|
|CC, SCC|Returns January 1, cc01 where cc is first 2 digits of the given year if last 2 digits <= 50, or 1 greater than the first 2 digits of the given year if last 2 digits \> 50; \(for AD years\)|
|SYYY, YYYY, YEAR, SYEAR, YYY, YY, Y|Returns January 1, yyyy where yyyy is rounded to the nearest year; rounds down on June 30, rounds up on July 1|
|IYYY, IYY, IY, I|Rounds to the beginning of the ISO year which is determined by rounding down if the month and day is on or before June 30th, or by rounding up if the month and day is July 1st or later|
|Q|Returns the first day of the quarter determined by rounding down if the month and day is on or before the 15th of the second month of the quarter, or by rounding up if the month and day is on the 16th of the second month or later of the quarter|
|MONTH, MON, MM, RM|Returns the first day of the specified month if the day of the month is on or prior to the 15th; returns the first day of the following month if the day of the month is on the 16th or later|
|WW|Round to the nearest date that corresponds to the same day of the week as the first day of the year|
|IW|Round to the nearest date that corresponds to the same day of the week as the first day of the ISO year|
|W|Round to the nearest date that corresponds to the same day of the week as the first day of the month|
|DDD, DD, J|Rounds to the start of the nearest day; 11:59:59 AM or earlier rounds to the start of the same day; 12:00:00 PM or later rounds to the start of the next day|
|DAY, DY, D|Rounds to the nearest Sunday|
|HH, HH12, HH2 4|Round to the nearest hour|
|MI|Round to the nearest minute|

下面是函数ROUND的使用示例。

下面的示例将日期取整到与之最接近的世纪的开始年份。

``` {#codeblock_gqy_v5p_kdu}
SELECT TO_CHAR(ROUND(TO_DATE('1950','YYYY'),'CC'),'DD-MON-YYYY') "Century" FROM DUAL;

   Century
-------------
 01-JAN-1901
(1 row)

SELECT TO_CHAR(ROUND(TO_DATE('1951','YYYY'),'CC'),'DD-MON-YYYY') "Century" FROM DUAL;

   Century
-------------
 01-JAN-2001
(1 row)	
```

下面的示例将日期取整到与之最近年份的开始日期。

``` {#codeblock_xp5_bfs_kbm}
SELECT TO_CHAR(ROUND(TO_DATE('30-JUN-1999','DD-MON-YYYY'),'Y'),'DD-MON-YYYY') "Year" FROM DUAL;

    Year
-------------
 01-JAN-1999
(1 row)

SELECT TO_CHAR(ROUND(TO_DATE('01-JUL-1999','DD-MON-YYYY'),'Y'),'DD-MON-YYYY') "Year" FROM DUAL;

    Year
-------------
 01-JAN-2000
(1 row)	
```

下面的示例将日期取整到与之最接近ISO年份的开始日期。第一个示例把日期取整为2004年，对于2004年的ISO年份来说，实际上是在2003年12月29号开始。第二个示例把日期取整到2005年。对于2005年的ISO年份来说，实际上是在2005年的1月3号开始。

**说明：** ISO年份是以7天为跨度从第一个星期一开始，从星期一到星期日，包含新的一年里至少4天的日期。因此，可以从前一年的12月开始一个ISO年份。

``` {#codeblock_2q8_43g_oqm}
SELECT TO_CHAR(ROUND(TO_DATE('30-JUN-2004','DD-MON-YYYY'),'IYYY'),'DD-MON-YYYY') "ISO Year" FROM DUAL;

  ISO Year
-------------
 29-DEC-2003
(1 row)

SELECT TO_CHAR(ROUND(TO_DATE('01-JUL-2004','DD-MON-YYYY'),'IYYY'),'DD-MON-YYYY') "ISO Year" FROM DUAL;

  ISO Year
-------------
 03-JAN-2005
(1 row)	
```

下面的示例把日期取整到与之最接近的季度。

``` {#codeblock_k3h_7cf_eqi}
SELECT ROUND(TO_DATE('15-FEB-07','DD-MON-YY'),'Q') "Quarter" FROM DUAL;

      Quarter
--------------------
 01-JAN-07 00:00:00
(1 row)

SELECT ROUND(TO_DATE('16-FEB-07','DD-MON-YY'),'Q') "Quarter" FROM DUAL;

      Quarter
--------------------
 01-APR-07 00:00:00
(1 row)	
```

下面的示例将日期取整与之到最近的月份。

``` {#codeblock_dds_alz_pwy}
SELECT ROUND(TO_DATE('15-DEC-07','DD-MON-YY'),'MONTH') "Month" FROM DUAL;

       Month
--------------------
 01-DEC-07 00:00:00
(1 row)

SELECT ROUND(TO_DATE('16-DEC-07','DD-MON-YY'),'MONTH') "Month" FROM DUAL;

       Month
--------------------
 01-JAN-08 00:00:00
(1 row)
```

下面的示例将日期取整与之最接近的星期。所以在第一个示例中，与2007年1月18日最接近的星期一是2007年1月15日。在第二个示例中，与2007年1月19日最接近的星期一是2007年1月22日。

``` {#codeblock_k20_tcf_t2u}
SELECT ROUND(TO_DATE('18-JAN-07','DD-MON-YY'),'WW') "Week" FROM DUAL;

        Week
--------------------
 15-JAN-07 00:00:00
(1 row)

SELECT ROUND(TO_DATE('19-JAN-07','DD-MON-YY'),'WW') "Week" FROM DUAL;

        Week
--------------------
 22-JAN-07 00:00:00
(1 row)	
```

下面的示例把日期取整与之到最近的以ISO格式表示的星期数。以ISO格式表示的周数从星期一开始，在第一个示例中，与日期2004年1月1日是最接近的星期一是2003年12月29日。在第二个示例中，与2004年1月2日最接近的星期一是2004年1月5日。

``` {#codeblock_46h_v5e_auf}
SELECT ROUND(TO_DATE('01-JAN-04','DD-MON-YY'),'IW') "ISO Week" FROM DUAL;

      ISO Week
--------------------
 29-DEC-03 00:00:00
(1 row)

SELECT ROUND(TO_DATE('02-JAN-04','DD-MON-YY'),'IW') "ISO Week" FROM DUAL;

      ISO Week
--------------------
 05-JAN-04 00:00:00
(1 row)		
```

下面的示例把日期值取整到与之最接近的一周，其中周的开始日期被认为是和每月第一天相同。

``` {#codeblock_ecx_7sj_5mm}
SELECT ROUND(TO_DATE('05-MAR-07','DD-MON-YY'),'W') "Week" FROM DUAL;

        Week
--------------------
 08-MAR-07 00:00:00
(1 row)

SELECT ROUND(TO_DATE('04-MAR-07','DD-MON-YY'),'W') "Week" FROM DUAL;

        Week
--------------------
 01-MAR-07 00:00:00
(1 row)	
```

下面的示例把日期值取整到与之最接近的日期。

``` {#codeblock_su7_tvi_xee}
SELECT ROUND(TO_DATE('04-AUG-07 11:59:59 AM','DD-MON-YY HH:MI:SS AM'),'J') "Day" FROM DUAL;

        Day
--------------------
 04-AUG-07 00:00:00
(1 row)

SELECT ROUND(TO_DATE('04-AUG-07 12:00:00 PM','DD-MON-YY HH:MI:SS AM'),'J') "Day" FROM DUAL;

        Day
--------------------
 05-AUG-07 00:00:00
(1 row)
```

下面的示例把日期值取整到与之最接近，周日期为星期天的日期。

``` {#codeblock_zmz_ug4_rie}
SELECT ROUND(TO_DATE('08-AUG-07','DD-MON-YY'),'DAY') "Day of Week" FROM DUAL;

    Day of Week
--------------------
 05-AUG-07 00:00:00
(1 row)

SELECT ROUND(TO_DATE('09-AUG-07','DD-MON-YY'),'DAY') "Day of Week" FROM DUAL;

    Day of Week
--------------------
 12-AUG-07 00:00:00
(1 row)
```

下面的示例把日期值取整到与之最接近的小时值。

``` {#codeblock_7v1_k2x_cy4}
SELECT TO_CHAR(ROUND(TO_DATE('09-AUG-07 08:29','DD-MON-YY HH:MI'),'HH'),'DD-MON-YY HH24:MI:SS') "Hour" FROM DUAL;

        Hour
--------------------
 09-AUG-07 08:00:00
(1 row)

SELECT TO_CHAR(ROUND(TO_DATE('09-AUG-07 08:30','DD-MON-YY HH:MI'),'HH'),'DD-MON-YY HH24:MI:SS') "Hour" FROM DUAL;

        Hour
--------------------
 09-AUG-07 09:00:00
(1 row)
```

下面的示例把日期值取整到与之最接近的分钟值。

``` {#codeblock_xln_7l3_jqv}
SELECT TO_CHAR(ROUND(TO_DATE('09-AUG-07 08:30:29','DD-MON-YY HH:MI:SS'),'MI'),'DD-MON-YY HH24:MI:SS') "Minute" FROM DUAL;

       Minute
--------------------
 09-AUG-07 08:30:00
(1 row)

SELECT TO_CHAR(ROUND(TO_DATE('09-AUG-07 08:30:30','DD-MON-YY HH:MI:SS'),'MI'),'DD-MON-YY HH24:MI:SS') "Minute" FROM DUAL;

       Minute
--------------------
 09-AUG-07 08:31:00
(1 row)
```

