# MONTHS\_BETWEEN {#concept_221789 .concept}

函数MONTHS\_BETWEEN返回2个日期之间的月数。如果第一个日期大于第二个日期，那么返回结果是一个正数数值，反之，返回结果则是一个负数。

如果所有日期参数中月份的日期相同，或者所有日期参数分别是月份中的最后一天，那么结果就是整的月数。

下面是函数MONTHS\_BETWEEN的一些示例。

``` {#codeblock_msg_9a5_296}
SELECT MONTHS_BETWEEN('15-DEC-06','15-OCT-06') FROM DUAL;

 months_between
----------------
              2
(1 row)

SELECT MONTHS_BETWEEN('15-OCT-06','15-DEC-06') FROM DUAL;

 months_between
----------------
             -2
(1 row)

SELECT MONTHS_BETWEEN('31-JUL-00','01-JUL-00') FROM DUAL;

 months_between
----------------
    0.967741935
(1 row)

SELECT MONTHS_BETWEEN('01-JAN-07','01-JAN-06') FROM DUAL;

 months_between
----------------
             12
(1 row)	
```

