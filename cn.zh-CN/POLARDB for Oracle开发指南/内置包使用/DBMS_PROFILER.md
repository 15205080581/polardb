# DBMS\_PROFILER {#concept_221984 .concept}

DBMS\_PROFILER包收集并存储在性能剖析会话中执行的关于PL/pgSQL和SPL语句的性能信息。我们可以使用下列表中列出的函数和存储过程来控制剖析工具。

|Function/Procedure|Function or Procedure|Return Type|Description|
|------------------|---------------------|-----------|-----------|
|FLUSH DATA|Both|Status Code or Exception|Flushes performance data collected in the current session without terminating the session \(profiling continues\).|
|GET VERSION\(major OUT, minor OUT\)|Procedure|n/a|Returns the version number of this package.|
|INTERNAL VERSION CHECK|Function|Status Code|Confirms that the current version of the profiler will work with the current database.|
|PAUSE PROFILER|Both|Status Code or Exception|Pause data collection.|
|PAUSE PROFILER|Both|Status Code or Exception|Resume data collection.|
|START PROFILER\(run comment, run commentl \[, run number OUT \]\)|Both|Status Code or Exception|Start data collection.|
|STOP PROFILER|Both|Status Code or Exception|Stop data collection and flush performance data to the PLSQL PROFILER RAWDATA table.|

DBMS\_PROFILER包中的函数返回的是一个表明成功或失效的状态码。只有在DBMS\_PROFILER存储过程遇到失效时，DBMS\_PROFILER存储过程才会产生异常。下列表中列出了由函数返回的状态码和消息，以及存储过程产生的异常。

|Status Code|Message|Exception|Description|
|-----------|-------|---------|-----------|
|-1|error version|version\_mismatch|The profiler version and the database are incompatible.|
|0|success|n/a|The operation completed successfully.|
|1|error\_param|profiler\_error|The operation received an incorrect parameter.|
|2|error\_io|profiler\_error|The data flush operation has failed.|

## FLUSH\_DATA {#section_7z3_jex_fdt .section}

在不终结分析器会话的情况下，FLUSH\_DATA函数/存储过程会刷新从当前会话中收集的数据。数据将被刷新到POLARDB for Oracle性能特性指南描述的表中。FLUSH\_DATA函数和存储过程的语法如下：

``` {#codeblock_ly8_ss1_166}
status INTEGER FLUSH_DATA

FLUSH_DATA
```

**参数**

|参数名称|描述|
|----|--|
|status|状态码是由运算返回的。|

## GET\_VERSION {#section_u6c_6ce_ng9 .section}

GET\_VERSION 存储过程返回的是DBMS\_PROFILER版本的存储过程。语法如下：

``` {#codeblock_tvk_s9s_iac}
GET_VERSION(major OUT INTEGER, minor OUT INTEGER)
```

**参数**

|参数名称|描述|
|----|--|
|major|DBMS\_PROFILER 主要版本的数量。|
|minor|DBMS\_PROFILER 次要版本的数量。|

## INTERNAL\_VERSION\_CHECK {#section_o00_m47_h9s .section}

The INTERNAL\_VERSION\_CHECK 函数用于确认DBMS\_PROFILER的当前版本是否能与当前数据库工作。函数语法如下：

``` {#codeblock_hei_lzx_2pn}
status INTEGER INTERNAL_VERSION_CHECK
```

**参数**

|参数名称|描述|
|----|--|
|status|状态码是由运算返回的。|

## PAUSE\_PROFILER {#section_ogg_u50_9q9 .section}

PAUSE\_PROFILER函数/存储过程用于暂停分析会话。语法如下：

``` {#codeblock_6su_ary_987}
status INTEGER PAUSE_PROFILER

PAUSE_PROFILER
```

**参数**

|参数名称|描述|
|----|--|
|status|状态码是由运算返回的。|

## RESUME\_PROFILER {#section_qcx_1k3_9m0 .section}

RESUME\_PROFILER 函数/存储过程用于继续分析会话。RESUME\_PROFILER 函数/存储过程语法如下：

``` {#codeblock_smu_ry6_4k2}
status INTEGER RESUME_PROFILER

RESUME_PROFILER
```

**参数**

|参数名称|描述|
|----|--|
|status|状态码是由运算返回的。|

## START\_PROFILER {#section_va9_j2w_hsj .section}

START\_PROFILER函数/存储过程用于开始数据收集会话。语法如下：

``` {#codeblock_y4l_9c7_pgy}
status INTEGER START_PROFILER(run_comment TEXT := SYSDATE,
  run_comment1 TEXT := '' [, run_number OUT INTEGER ])

START_PROFILER(run_comment TEXT := SYSDATE,
  run_comment1 TEXT := '' [, run_number OUT INTEGER ])
```

**参数**

|参数名称|描述|
|----|--|
|run comment|给分析器会话的用户定义的注释。缺省值为SYSDATE。|
|run commentl|给分析器会话的额外用户定义的注释。缺省值为TT。|
|run number|分析器会话的数量。|
|status|状态码是由运算返回的。|

## STOP\_PROFILER {#section_71b_vm6_wwn .section}

STOP\_PROFILER函数/存储过程用于停止分析会话及刷新性能信息到DBMS\_PROFILER表和视图中。语法如下：

``` {#codeblock_bib_zy7_dth}
status INTEGER STOP_PROFILER

STOP_PROFILER
```

**参数**

|参数名称|描述|
|----|--|
|status|状态码是由运算返回的。|

