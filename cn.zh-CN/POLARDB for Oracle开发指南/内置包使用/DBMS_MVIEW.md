# DBMS\_MVIEW {#concept_221981 .concept}

我们可以使用DBMS\_MVIEW包中的存储过程来管理、更新物化视图及它们的依赖关系。POLARDB for Oracle支持下列DBMS\_MVIEW存储过程：

|Procedure|Return Type|Description|
|---------|-----------|-----------|
|GET\_MV\_DEPENDENCIES\(list VARCHAR2, deplist VARCHAR2\);|n/a|The GET\_MV\_DEPENDENCIES procedure returns a list of dependencies for a specified view.|
|REFRESH\(list VARCHAR2, method VARCHAR2, rollback seg VARCHAR2 , push deferred rpc BOOLEAN, refresh after errors BOOLEAN , purge option NUMBER, parallelism NUMBER, heap size NUMBER , atomic refresh BOOLEAN , nested BOOLEAN\);|n/a|This variation of the REFRESH procedure refreshes all views named in a comma- separated list of view names.|
|REFRESH\(tab dbms\_utility.uncl\_array, method VARCHAR2, rollback\_seg VARCHAR2, push\_deferred\_rpc BOOLEAN, refresh\_after\_errors BOOLEAN, purge\_option NUMBER, parallelism NUMBER, heap\_size NUMBER, atomic\_refresh BOOLEAN, nested BOOLEAN\);|n/a|This variation of the REFRESH procedure refreshes all views named in a table of dbms\_utility.uncl\_array values.|
|REFRESH\_ALL\_MVIEWS\(number\_of\_failures BINARY\_INTEGER, method VARCHAR2, rollback\_seg VARCHAR2, refresh\_after\_errors BOOLEAN, atomic\_refresh BOOLEAN\);|n/a|The REFRESH\_ALL\_MVIEWS procedure refreshes all materialized views.|
|REFRESH\_DEPENDENT\(number\_of\_failures BINARY\_INTEGER, list VARCHAR2, method VARCHAR2, rollback\_seg VARCHAR2, refresh\_after\_errors BOOLEAN, atomic\_refresh BOOLEAN, nested BOOLEAN\);|n/a|This variation of the REFRESH\_DEPENDENT procedure refreshes all views that are dependent on the views listed in a comma-separated list.|
|REFRESH\_DEPENDENT\(number\_of\_failures BINARY\_INTEGER, tab dbms\_utility.uncl\_array, method VARCHAR2, rollback\_seg VARCHAR2, refresh\_after\_errors BOOLEAN, atomic\_refresh BOOLEAN, nested BOOLEAN\);|n/a|This variation of the REFRESH\_DEPENDENT procedure refreshes all views that are dependent on the views listed in a table of dbms\_utility.uncl\_array values.|

与Oracle版本的DBMS\_MVIEW执行相比，POLARDB for Oracle的DBMS\_MVIEW执行是部分执行。POLARDB for Oracle仅支持上述表中列出的函数和存储过程。

## GET\_MV\_DEPENDENCIES {#section_f33_11w_2iy .section}

当命名一个物化视图之后，GET\_MV\_DEPENDENCIES返回的是依赖于指定视图的列表项。语法如下：

``` {#codeblock_qa3_3a4_erm}
GET_MV_DEPENDENCIES(
  list IN VARCHAR2, 
  deplist OUT VARCHAR2);
```

**参数**

|参数名称|描述|
|----|--|
|list|list 用于指定物化视图的名称或物化视图名称中用逗号分隔的列表。|
|deplist|deplist 是一个模式限定依赖关系中用逗号分隔的列表。 **说明：** deplist 是一个VARCHAR2 值。

 |

**示例**

``` {#codeblock_zaz_2ld_t0q}
DECLARE
  deplist VARCHAR2(1000);
BEGIN
  DBMS_MVIEW.GET_MV_DEPENDENCIES('public.emp_view', deplist);
  DBMS_OUTPUT.PUT_LINE('deplist: ' || deplist);
END;
```

显示了物化视图public. emp\_view上的依赖关系列表。

## REFRESH {#section_eyi_8e5_4pp .section}

我们可以使用REFRESH存储过程来更新在用逗号分隔的视图名称列表中或在DBMS\_UTILITY. UNCL\_ARRAY值的表中指定的所有视图。REFRESH存储过程有两种形式的语法。当我们指定逗号分隔的试图名称列表时，可以使用第一种形式的语法：

``` {#codeblock_qah_0bl_94j}
REFRESH(
  list IN VARCHAR2, 
  method IN VARCHAR2 DEFAULT NULL, 
  rollback_seg IN VARCHAR2 DEFAULT NULL, 
  push_deferred_rpc IN BOOLEAN DEFAULT TRUE, 
  refresh_after_errors IN BOOLEAN DEFAULT FALSE, 
  purge_option IN NUMBER DEFAULT 1, 
  parallelism IN NUMBER DEFAULT 0, 
  heap_size IN NUMBER DEFAULT 0, 
  atomic_refresh IN BOOLEAN DEFAULT TRUE, 
  nested IN BOOLEAN DEFAULT FALSE);
```

第二种形式的语法用于指定DBMS\_UTILITY . UNCL\_ARRAY值的表中的视图名称：

``` {#codeblock_xg0_9g1_o3a}
REFRESH(
  tab IN OUT DBMS_UTILITY.UNCL_ARRAY, 
  method IN VARCHAR2 DEFAULT NULL, 
  rollback_seg IN VARCHAR2 DEFAULT NULL, 
  push_deferred_rpc IN BOOLEAN DEFAULT TRUE, 
  refresh_after_errors IN BOOLEAN DEFAULT FALSE, 
  purge_option IN NUMBER DEFAULT 1, 
  parallelism IN NUMBER DEFAULT 0, 
  heap_size IN NUMBER DEFAULT 0, 
  atomic_refresh IN BOOLEAN DEFAULT TRUE, 
  nested IN BOOLEAN DEFAULT FALSE);
```

**参数**

|参数名称|描述|
|----|--|
|list|list 是一个VARCHAR2 值。用于指定物化视图的名称或逗号分隔的物化视图名称列表，且名称必须是模式限定的。|
|tab|tab 是DBMS\_UTILITY .UNCL\_ARRAY 值的表，用于指定物化视图的名称。|
|method|method 是一个 VARCHAR2 值。用于指定将要应用于指定视图的更新方法。C 是唯一支持的更新方法，它能将视图完整地更新。|
|rollback seg|rollback\_seg 可被兼容和忽略。缺省为NULL 。|
|push deferred rpc|push\_deferred\_rpc 可被兼容和忽略。缺省为TRUE。|
|refresh after errors|refresh\_after\_errors 可被兼容和忽略。缺省为FALSE。|
|purge option|purge\_option 可被兼容和忽略。缺省为1。|
|parallelism|parallelism可被兼容和忽略。缺省为0。|
|heap\_size IN NUMBER DEFAULT 0,|heap\_size可被兼容和忽略。缺省为0。|
|atomic refresh|atomic\_refresh可被兼容和忽略。缺省为TRUE。|
|nested|nested可被兼容和忽略。缺省为FALSE。|

**示例**

下列示例使用了DBMS\_MVIEW.REFRESH 对物化视图public.emp\_view 进行COMPLETE 更新操作：

``` {#codeblock_h74_2t9_fyl}
EXEC DBMS_MVIEW.REFRESH(list => 'public.emp_view', method => 'C');
```

## REFRESH\_ALL\_M VIEWS {#section_1mb_d1j_34b .section}

表或视图的视图关系修改之后，我们可以使用REFRESH\_ALL\_MVIEWS存储过程来更新任何没有被更新的物化视图。语法如下：

``` {#codeblock_ubl_1gi_jei}
REFRESH_ALL_MVIEWS(
  number_of_failures OUT BINARY_INTEGER, 
  method IN VARCHAR2 DEFAULT NULL, 
  rollback_seg IN VARCHAR2 DEFAULT NULL, 
  refresh_after_errors IN BOOLEAN DEFAULT FALSE, 
  atomic_refresh IN BOOLEAN DEFAULT TRUE);
```

**参数**

|参数名称|描述|
|----|--|
|number of failures|number\_of\_failures 是一个BINARY\_INTEGER，用于指定在更新操作中发生的失效数量。|
|method|method 是一个 VARCHAR2 值。用于指定将要应用于指定视图的更新方法。C 是唯一支持的更新方法，它能将视图完整地更新。|
|rollback seg|rollback\_seg可被兼容和忽略。缺省为NULL。|
|refresh after errors|refresh\_after\_errors可被兼容和忽略。缺省为FALSE。|
|atomic refresh|atomic\_refresh is可被兼容和忽略。缺省为TRUE。|

**示例**

``` {#codeblock_9vw_izf_g50}
DECLARE
  errors INTEGER;
BEGIN
  DBMS_MVIEW.REFRESH_ALL_MVIEWS(errors, method => 'C');
END;
```

更新完成后，errors 就会包含失效数量。

## REFRESH\_DEPENDENT {#section_4ij_5es_irj .section}

我们可以使用REFRESH\_DEPENDENT存储过程来更新所有的物化视图，这些物化视图是依赖于对存储过程调用时指定视图上的。我们可以指定一个逗号分隔的列表或在DBMS\_UTILITY. UNCL\_ARRAY值的表中提供视图名称。

使用第一种存储过程的形式来更新所有物化视图，这些物化视图是依赖于在逗号分隔的列表中指定视图上的：

``` {#codeblock_mgx_3u1_ofh}
REFRESH_DEPENDENT(
  number_of_failures OUT BINARY_INTEGER,
  list IN VARCHAR2,
  method IN VARCHAR2 DEFAULT NULL,
  rollback_seg IN VARCHAR2 DEFAULT NULL
  refresh_after_errors IN BOOLEAN DEFAULT FALSE,
  atomic_refresh IN BOOLEAN DEFAULT TRUE,
  nested IN BOOLEAN DEFAULT FALSE);
```

使用第二种存储过程的形式来更新所有物化视图，这些物化视图是依赖于DBMS\_UTILITY. UNCL\_ARRAY值的表中指定视图上的：

``` {#codeblock_1rj_7ua_226}
REFRESH_DEPENDENT(
  number_of_failures OUT BINARY_INTEGER, 
  tab IN DBMS_UTILITY.UNCL_ARRAY, 
  method IN VARCHAR2 DEFAULT NULL, 
  rollback_seg IN VARCHAR2 DEFAULT NULL,
  refresh_after_errors IN BOOLEAN DEFAULT FALSE, 
  atomic_refresh IN BOOLEAN DEFAULT TRUE, 
  nested IN BOOLEAN DEFAULT FALSE);
```

**参数**

|参数名称|描述|
|----|--|
|number of failures|number\_of\_failures 是一个BINARY\_INTEGER，它包含了在更新操作中发生的失效数量。|
|list|list 是一个VARCHAR2 值。用于指定物化视图的名称或逗号分隔的物化视图名称列表，且名称必须是模式限定的。|
|tab|tab 是一个DBMS\_UTILITY .UNCL\_ARRAY 值的表，用于指定物化视图的名称。|
|method|method 是一个 VARCHAR2 值。用于指定将要应用于指定视图的更新方法。C 是唯一支持的更新方法，它能将视图完整地更新。|
|rollback seg|rollback\_seg可被兼容和忽略。缺省为NULL。|
|refresh after errors|refresh\_after\_errors可被兼容和忽略。缺省为FALSE。|
|atomic refresh|atomic\_refresh 可被兼容和忽略。缺省TRUE。|
|nested|nested 可被兼容和忽略。缺省为FALSE。|

**示例**

下列示例对所有物化视图进行了COMPLETE更新操作。所有这些物化视图依赖于一个名为emp\_view的物化视图，且物化视图emp\_view所属于公有模式。

``` {#codeblock_tp5_z8g_1z0}
DECLARE
  errors INTEGER;
BEGIN
  DBMS_MVIEW.REFRESH_DEPENDENT(errors, list => 'public.emp_view', method => 'C');
END;
```

更新完成后，errors 就包含了失效数量。

