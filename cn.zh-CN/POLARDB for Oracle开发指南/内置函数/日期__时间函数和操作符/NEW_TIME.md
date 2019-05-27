# NEW\_TIME {#concept_221793 .concept}

函数NEW\_TIME用于将一个日期和时间值从一个时区转换到另外一个时区。这个函数返回值类型为DATE。语法如下：

``` {#codeblock_e5p_nlx_7wy}
NEW_TIME(DATE, time_zone1, time_zone2)
```

其中参数time\_zone1和time\_zone2必须是从下面列表中列Time Zone中取出的字符串类型 值。

|Time Zone|Offset from UTC|Description|
|---------|---------------|-----------|
|AST|UTC+4|Atlantic Standard Time|
|ADT|UTC+3|Atlantic Daylight Time|
|BST|UTC+11|Bering Standard Time|
|BDT|UTC+10|Bering Daylight Time|
|CST|UTC+6|Central Standard Time|
|CDT|UTC+5|Central Daylight Time|
|EST|UTC+5|Eastern Standard Time|
|EDT|UTC+4|Eastern Daylight Time|
|GMT|UTC|Greenwich Mean Time|
|HST|UTC+10|Alaska-Hawaii Standard Time|
|HDT|UTC+9|Alaska-Hawaii Daylight Time|
|MST|UTC+7|Mountain Standard Time|
|MDT|UTC+6|Mountain Daylight Time|
|NST|UTC+3:30|Newfoundland Standard Time|
|PST|UTC+8|Pacific Standard Time|
|PDT|UTC+7|Pacific Daylight Time|
|YST|UTC+9|Yukon Standard Time|
|YDT|UTC+8|Yukon Daylight Time|

下面是一个关于函数NEW\_TIME的示例：

``` {#codeblock_g6v_2yj_tc0}
SELECT NEW_TIME(TO_DATE('08-13-07 10:35:15','MM-DD-YY HH24:MI:SS'),'AST', 'PST') "Pacific Standard Time" FROM DUAL;

Pacific Standard Time
---------------------  
 13-AUG-07 06:35:15
(1 row)
```

