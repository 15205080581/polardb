# DBMS\_LOCK {#concept_221980 .concept}

POLARDB for Oracle支持DBMS\_LOCK.SLEEP 存储过程。

|Function/Procedure|Return Type|Description|
|------------------|-----------|-----------|
|SLEEP\(seconds\)|n/a|Suspends a session for the specified number of seconds.|

与Oracle版本的DBMS\_LOCK执行相比，POLARDB for Oracle的DBMS\_LOCK执行是部分执行。POLARDB for Oracle仅支持DBMS\_LOCK.SLEEP。

## SLEEP {#section_2cl_w6f_g21 .section}

SLEEP存储过程用于暂停当前会话,暂停时长为我们指定的秒数。

``` {#codeblock_uln_z05_pjk}
SLEEP(seconds NUMBER)
```

**参数**

|参数名称|描述|
|----|--|
|seconds|Seconds用于指定我们想要暂停会话的秒数时长. Seconds可以是一个小数值.例如,输入1.75来指定1又3/4秒。|

