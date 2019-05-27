# NEXT\_DAY {#concept_221790 .concept}

函数NEXT\_DAY返回大于指定日期参数的第一个周日期。我们应该至少指定周日期的前三个字母--例如SAT,如果日期中包括时间部分，那么对结果没有影响。

下面是函数NEXT\_DAY的示例。

``` {#codeblock_e9y_gp8_237}
SELECT NEXT_DAY(TO_DATE('13-AUG-07','DD-MON-YY'),'SUNDAY') FROM DUAL;

      next_day
--------------------
 19-AUG-07 00:00:00
(1 row)

SELECT NEXT_DAY(TO_DATE('13-AUG-07','DD-MON-YY'),'MON') FROM DUAL;

      next_day
--------------------
 20-AUG-07 00:00:00
(1 row)	
```

