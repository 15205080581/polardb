# ADD\_MONTHS {#concept_221781 .concept}

函数ADD\_MONTHS在指定的日期上加上（如果第二个参数是负数，那么就是减）指定月数。在执行 结果中日期和在给定日期中月份的日期是相同的，除非指定日期是月份的最后一天，在这种情况下 ，所得到的结果日期永远是执行结果中月份的最后一天。

**说明：** 

-   在执行计算前，将截断月份参数的小数部分。
-   如果日期包含时间部分，这对结果没有影响。

## 示例 {#section_dii_kob_rwv .section}

``` {#codeblock_j6o_3de_0up}
SELECT ADD_MONTHS('13-JUN-07',4) FROM DUAL;

     add_months
--------------------
 13-OCT-07 00:00:00
(1 row)

SELECT ADD_MONTHS('31-DEC-06',2) FROM DUAL;

     add_months
--------------------
 28-FEB-07 00:00:00
(1 row)


SELECT ADD_MONTHS('31-MAY-04',-3) FROM DUAL;

     add_months
--------------------
 29-FEB-04 00:00:00
(1 row)	
```

