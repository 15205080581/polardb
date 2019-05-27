# DBMS\_RLS {#concept_221986 .concept}

DBMS\_RLS包可以使虚拟私有数据库执行于特定的POLARDB for Oracle数据库对象上。

|Function/Procedure|Function or Procedure|Return Type|Description|
|------------------|---------------------|-----------|-----------|
|ADD POLICY\(object schema, object name, policy name, function schema, policy function \[, statement types \[, update check \[, enable \[, static policy \[, policy type \[, long predicate \[, sec relevant cols \[, sec relevant cols opt \]\]\]\]\]\]\]\]\)|Procedure|n/a|Add a security policy to a database object.|
|DROP\_POLICY\(object\_schema, object\_name, policy\_name\)|Procedure|n/a|Remove a security policy from a database object.|
|ENABLE\_POLICY\(object\_schema, object\_name, policy\_name, enable\)|Procedure|n/a|Enable or disable a security policy.|

与Oracle版本的DBMS\_RLS包执行相比，POLARDB for Oracle的DBMS\_RLS包执行是一个部分执行。POLARDB for Oracle仅支持上述表中列出的函数和存储过程。

虚拟私有数据库是一种使用安全政策的细粒度访问控制。正如安全政策所定义的那样，虚拟私有数据库中的细粒度访问控制意味着对于数据的访问可以控制到具体的行信息。

在policy function中定义了编码安全政策的规则。这个规则其实是一个SPL函数，有特定的输入参数和返回值。security policy是命名的政策函数联合到特定的数据库对象，尤其是表。

**说明：** 

-   在POLARDB for Oracle中，可以用任何POLARDB for Oracle所支持的语言来编写政策函数。例如，除了与Oracle兼容的SPL语言外，我们还可以使用SQL 和 PL/pgSQL语言。
-   目前POLARDB for Oracle虚拟私有数据库所支持的数据库对象为表。政策不适用于视图或同义词。

使用虚拟私有数据库的优势有以下几点：

-   虚拟私有数据库可以提供细粒度级别的访问安全。GRANT命令授予的数据库对象级别的权限能够决定访问权限是否能访问数据库对象中的整个实例。虚拟私有数据库则为数据库对象实例的个人记录提供了访问控制。
-   根据SQL命令（INSERT、UPDATE、DELETE、或 SELECT）的类型，我们可以应用不同的安全政策。
-   由于每个可应用的SQL命令影响的数据库对象取决于一些因素（例如申请访问数据库对象的会话用户），因此安全政策会动态变化。
-   安全政策的调用对所有数据库对象的访问申请都是透明的。因此，我们不用为了应用安全政策去修改个人申请。
-   一旦启用了安全政策，那么任何申请（包括新申请）都无法绕过安全政策。除下列注解中列出的系统权限以外。
-   除下列注解中列出的系统权限以外，即使是超级用户也不能绕过安全政策。

**说明：** 唯一可以绕过安全政策的方法就是授权给用户EXEMPT ACCESS POLICY系统权限。但EXEMPT ACCESS POLICY系统权限的授予必须格外小心，因为有此权限的用户可以绕过数据库中所有的安全政策。

DBMS\_RLS包提供的存储过程可用于创建、删除、启用及禁用安全政策。

执行虚拟私有数据库的步骤如下：

-   首先要创建一个政策函数。这个函数必须有两个类型VARCHAR2的输入参数。第一个输入参数提供给包含数据库对象（安全政策要应用于这个数据库对象上）的模式。第二个输入参数则提供给数据库对象的名称。所创建的这个政策函数还必须有一个VARCHAR2返回类型，且返回的必须是一个WHERE谓语子句形式的字符串。谓语将以AND条件动态附于对数据库对象起作用的SQL命令之上。因此，不满足政策函数谓语的记录将从SQL命令的结果集中过滤掉。
-   使用ADD\_POLICY存储过程来定义一个新政策，这是政策函数与数据库对象的联合。通过使用ADD\_POLICY存储过程，我们可以指定SQL命令（例如：INSERT、 UPDATE、 DELETE 或 SELECT，且政策要应用于这些SQL命令之上）的类型，也可以决定是否在创建政策的同时对它进行启用，或决定政策函数是否可以应用于新插入的记录上或更新记录修改后的图像上。
-   使用ENABLE\_POLICY 存储过程来禁用或启用现有的安全政策。
-   使用DROP\_POLICY 存储过程来删除已有的政策。但DROP\_POLICY 存储过程不能删除政策函数或联合数据库对象。

一旦政策创建之后，我们就可以在与Oracle兼容的目录视图下浏览所创建的政策。

SYS\_CONTEXT 函数常与DBMS\_RLS一起使用。语法如下：

``` {#codeblock_jax_zj9_xk7}
SYS_CONTEXT(namespace, attribute)
			
```

-   `namespace` 是一个VARCHAR2值。唯一接受的值是USERENV。任何其他的值返回的都将是NULL。
-   `attribute`是一个VARCHAR2值。属性可能是。

    |attribute Value|Equivalent Value|
    |---------------|----------------|
    |SESSION\_USER|pg\_catalog.session\_user|
    |CURRENT\_USER|pg\_catalog.current\_user|
    |CURRENT\_SCHEMA|pg\_catalog.current\_schema|
    |HOST|pg\_catalog.inet\_host|
    |IP\_ADDRESS|pg\_catalog.inet\_client\_addr|
    |SERVER\_HOST|pg\_catalog.inet\_server\_addr|


**说明：** 用于说明DBMS\_RLS包的示例基于样本表emp的修改后的副本， 提供给表emp的POLARDB for Oracle及一个名为salesmgr的角色授予所有权限给这个表。如下所示，我们可以创建一个名为vpemp的表emp的副本及名为salesmgr的角色。

``` {#codeblock_lrq_4rz_8nn}
CREATE TABLE public.vpemp AS SELECT empno, ename, job, sal, comm, deptno FROM emp;
ALTER TABLE vpemp ADD authid VARCHAR2(12);
UPDATE vpemp SET authid = 'researchmgr' WHERE deptno = 20;
UPDATE vpemp SET authid = 'salesmgr' WHERE deptno = 30;
SELECT * FROM vpemp;

empno | ename  |    job    |   sal   |  comm   | deptno |   authid    
-------+--------+-----------+---------+---------+--------+-------------
  7782 | CLARK  | MANAGER   | 2450.00 |         |     10 | 
  7839 | KING   | PRESIDENT | 5000.00 |         |     10 | 
  7934 | MILLER | CLERK     | 1300.00 |         |     10 | 
  7369 | SMITH  | CLERK     |  800.00 |         |     20 | researchmgr
  7566 | JONES  | MANAGER   | 2975.00 |         |     20 | researchmgr
  7788 | SCOTT  | ANALYST   | 3000.00 |         |     20 | researchmgr
  7876 | ADAMS  | CLERK     | 1100.00 |         |     20 | researchmgr
  7902 | FORD   | ANALYST   | 3000.00 |         |     20 | researchmgr
  7499 | ALLEN  | SALESMAN  | 1600.00 |  300.00 |     30 | salesmgr
  7521 | WARD   | SALESMAN  | 1250.00 |  500.00 |     30 | salesmgr
  7654 | MARTIN | SALESMAN  | 1250.00 | 1400.00 |     30 | salesmgr
  7698 | BLAKE  | MANAGER   | 2850.00 |         |     30 | salesmgr
  7844 | TURNER | SALESMAN  | 1500.00 |    0.00 |     30 | salesmgr
  7900 | JAMES  | CLERK     |  950.00 |         |     30 | salesmgr
(14 rows)

CREATE ROLE salesmgr WITH LOGIN PASSWORD 'password';
GRANT ALL ON vpemp TO salesmgr;
```

## ADD\_POLICY {#section_ryv_82n_sij .section}

ADD\_POLICY 存储过程通过联合政策函数和数据库对象来创建一个新政策。

只有超级用户才能执行ADD\_POLICY 存储过程。

``` {#codeblock_9q9_z6f_f79}
ADD_POLICY(object_schema VARCHAR2, object_name VARCHAR2,
  policy_name VARCHAR2, function_schema VARCHAR2,
  policy_function VARCHAR2
  [, statement_types VARCHAR2
  [, update_check BOOLEAN
  [, enable BOOLEAN
  [, static_policy BOOLEAN
  [, policy_type INTEGER
  [, long_predicate BOOLEAN
  [, sec_relevant_cols VARCHAR2
  [, sec_relevant_cols_opt INTEGER ]]]]]]]])
```

**参数**

|参数名称|描述|
|----|--|
|object schema|包含数据库对象（政策将应用于这个数据库对象上）的模式名称。|
|object name|政策所要应用于的数据库对象的名称。也许会有1个以上的政策应用于一个指定的数据库对象上。|
|policy name|`policy name`是分配给政策的名称。数据库对象（由`object_schema`和`object_name`标识）的联接与政策名称在数据库中必须是的唯一的。|
|function schema|包含政策函数的模式名称。 **说明：** 政策函数也许属于一个包。在这种情况下，`function_schema`必须含有定义包的模式名称。

 |
|policy function|`policy function`是SPL函数的名称，用于定义安全政策的规则。相同的函数也许会指定于多个政策中。 **说明：** 政策函数也许属于一个包。在这种情况下，`policy_function`必须也包含点符号的包名称（也就是`package name`. `function name`）

 |
|statement types|`statement types`是逗号分隔的SQL命令列表，且政策应用于SQL命令之上。有效的SQL命令是`INSERT、UPDATE、DELETE、 和 SELECT`。缺省为`INSERT,UPDATE,DELETE,SELECT`。 **说明：** POLARDB for Oracle接受INDEX为语句类型，但会忽略。在POLARDB for Oracle中，政策不能应用于索引操作中。

 |
|update check|`update check`只能应用于INSERT 和UPDATE SQL 命令中。 -   当把`update check`设为true时，政策可应用于新插入的记录及更新记录修改后的图像上。如果根据政策函数谓语内容， 新的或修改后的记录不是模式限定的，那么insert 或update命令则会产生异常，并且不会插入或修改任何记录。
-   当把`update check`设为FALSE时，政策不可应用于新插入的记录或更新记录修改后的图像上。 因此，新插入的记录也许不会出现在SQL命令序列（SQL命令是调用相同政策的命令）的结果集中。同样的，根据UPDATE命令之前的政策，如果记录为模式限定的，那么记录将不会出现在SQL命令（调用相同的政策的SQL命令）的序列集中。

 |
|enable| -   当把`enable`设为TRUE时， 就启用了政策并将其应用到statement\_types参数指定的SQL命令中。
-   当把`enable`设为FALSE时，则禁用了政策且政策将不能应用于任何SQL命令中。通过使用ENABLE\_POLICY存储过程，可以启用政策。缺省为TRUE。

 |
|static policy| -   在Oracle环境下，当把static policy 设为TRUE时，政策是静态的。也就是说在数据库对象上的政策对每一个数据库对象进行第一次调用时，政策函数都会被评估一次。作为结果的政策函数谓语字符串会保存在内存中。当数据库服务器实例运行时，这些字符串可以为相同数据库对象上的相同政策的所有调用所再次使用。
-   在Oracle环境下，当把static policy 设为FALSE时，政策是动态的。也就是说政策函数会被重新评估，且政策函数谓语字符串也会为政策的所有调用而再次产生。
-   缺省为 FALSE。

 **说明：** 

-   在Oracle 10g中介绍了policy\_type 参数，它用于替换static\_policy 参数。在Oracle环境下，如果我们没有把policy\_type 参数设为它的缺省值NULL，那么policy\_type 参数设置将覆写static\_policy 设置。
-   POLARDB for Oracle 会忽略static\_policy 参数的设置。POLARDB for Oracle仅执行动态政策，而忽略static\_policy参数的设置。

 |
|policy type|在Oracle环境下，`policy type`用于决定重新评估政策函数的时间。因此，是否及何时由政策函数返回谓语字符串就改变了。缺省为NULL。 **说明：** `policy type`参数的设置会被POLARDB for Oracle忽略。POLARDB for Oracle通常会假设一个动态政策。

 |
|longpredicate|在Oracle环境下，如果把`longpredicate`设为TRUE，那么就能允许谓语达到32K字节。 否则，谓语就限制于4000字节。缺省为FALSE。 **说明：** `longpredicate`参数的设置会被POLARDB for Oracle忽略。一个POLARDB for Oracle政策函数能返回一个对于所有实际用途不限长度的谓语。

 |
|sec relevant cols|`sec relevant cols`是`object_name`列的逗号分隔的列表。它可以给列出的列提供列级别的虚拟私有数据库。如果所列出的列引用于`statement_types`中列出的SQL命令类型中，那么政策将被执行。如果没有引用这样的列，那么就不会执行政策。 缺省为NULL就像`sec relevant cols`包括了所有数据库对象的列一样，有相同的效果。

 |
|sec relevant cols opt|在Oracle环境下，如果将`sec_relevant_cols_opt`设为`DBMS_RLS.ALL_ROWS`（值1的INTEGER常量），那么在`sec_relevant_cols`中列出的列就会返回所有记录的NULL值。其中，记录中应用的政策谓语为假。（如果没有把`sec_relevant_cols_opt`设为`DBMS_RLS.ALL_ROWS`，那么结果集中将不会有这些记录返回。）缺省为NULL。 **说明：** POLARDB for Oracle不支持`DBMS_RLS.ALL_ROWS`的函数性。如果将`sec_relevant_cols_opt`设为`DBMS_RLS.ALL_ROWS`（1的INTEGER值），那么POLARDB for Oracle就会产生错误。

 |

**示例**

这个示例使用了以下政策函数：

``` {#codeblock_ohp_nga_0fn}
CREATE OR REPLACE FUNCTION verify_session_user (
    p_schema        VARCHAR2,
    p_object        VARCHAR2
)
RETURN VARCHAR2
IS
BEGIN
    RETURN 'authid = SYS_CONTEXT(''USERENV'', ''SESSION_USER'')';
END;
```

这个函数产生的谓语authid = SYS\_CONTEXT\('USERENV', 'SESSION\_USER'\)被添加到在ADD\_POLICY存储过程中指定类型的任何SQL命令的WHERE子句中。

这个函数对那些列authid内容与会话用户相同的记录限制了SQL命令的结果。

**说明：** 这个示例中使用的SYS\_CONTEXT函数用于返回登录用户名。在Oracle环境下，SYS\_CONTEXT函数用于返回一个application context的属性。SYS\_CONTEXT函数的第一个参数是一个应用上下文的名称。第二个参数则是应用上下文中的属性集的名称。USERENV是一个特殊的内置命名空间，用来描述当前会话。POLARDB for Oracle除支持SYS\_CONTEXT函数的特殊用法以外，不支持应用上下文。

下列匿名代码块对ADD\_POLICY存储过程进行了调用。从而创建名为secure\_update的政策。 通过使用函数verify\_session\_user，可以把政策secure\_update应用于表vpemp之上。无论在引用表vpemp时，是否给出了一个INSERT、 UPDATE 或 DELETE命令。

``` {#codeblock_65z_lmw_ab6}
DECLARE
    v_object_schema         VARCHAR2(30) := 'public';
    v_object_name           VARCHAR2(30) := 'vpemp';
    v_policy_name           VARCHAR2(30) := 'secure_update';
    v_function_schema       VARCHAR2(30) := 'enterprisedb';
    v_policy_function       VARCHAR2(30) := 'verify_session_user';
    v_statement_types       VARCHAR2(30) := 'INSERT,UPDATE,DELETE';
    v_update_check          BOOLEAN      := TRUE;
    v_enable                BOOLEAN      := TRUE;
BEGIN
    DBMS_RLS.ADD_POLICY(
        v_object_schema,
        v_object_name,
        v_policy_name,
        v_function_schema,
        v_policy_function,
        v_statement_types,
        v_update_check,
        v_enable
    );
END;
```

在成功创建政策之后，由用户salesmgr发起了一个终结会话。下列查询显示了表vpemp的内容。

``` {#codeblock_q20_2ox_w1p}
edb=# \c edb salesmgr
Password for user salesmgr: 
You are now connected to database "edb" as user "salesmgr".
edb=> SELECT * FROM vpemp;
 empno | ename  |    job    |   sal   |  comm   | deptno |   authid    
-------+--------+-----------+---------+---------+--------+-------------
  7782 | CLARK  | MANAGER   | 2450.00 |         |     10 | 
  7839 | KING   | PRESIDENT | 5000.00 |         |     10 | 
  7934 | MILLER | CLERK     | 1300.00 |         |     10 | 
  7369 | SMITH  | CLERK     |  800.00 |         |     20 | researchmgr
  7566 | JONES  | MANAGER   | 2975.00 |         |     20 | researchmgr
  7788 | SCOTT  | ANALYST   | 3000.00 |         |     20 | researchmgr
  7876 | ADAMS  | CLERK     | 1100.00 |         |     20 | researchmgr
  7902 | FORD   | ANALYST   | 3000.00 |         |     20 | researchmgr
  7499 | ALLEN  | SALESMAN  | 1600.00 |  300.00 |     30 | salesmgr
  7521 | WARD   | SALESMAN  | 1250.00 |  500.00 |     30 | salesmgr
  7654 | MARTIN | SALESMAN  | 1250.00 | 1400.00 |     30 | salesmgr
  7698 | BLAKE  | MANAGER   | 2850.00 |         |     30 | salesmgr
  7844 | TURNER | SALESMAN  | 1500.00 |    0.00 |     30 | salesmgr
  7900 | JAMES  | CLERK     |  950.00 |         |     30 | salesmgr
(14 rows)
```

用户salesmgr发起了一个非模式限定的UPDATE命令（没有WHERE子句）：

``` {#codeblock_imq_0sv_fhg}
edb=> UPDATE vpemp SET comm = sal * .75;
UPDATE 6
```

政策不会更新表中所有的记录，而是仅对那些authid列中含有salesmgr值的记录限制更新结果。其中，salesmgr值是由政策函数谓语authid = SYS\_CONTEXT\('USERENV', 'SESSION\_USER'\) 指定的。

下列查询显示了comm列仅为那些authid列中含有salesmgr的记录而进行改变。所有其他的记录不变 。

``` {#codeblock_kb5_uxk_8ui}
edb=> SELECT * FROM vpemp;
 empno | ename  |    job    |   sal   |  comm   | deptno |   authid    
-------+--------+-----------+---------+---------+--------+-------------
  7782 | CLARK  | MANAGER   | 2450.00 |         |     10 | 
  7839 | KING   | PRESIDENT | 5000.00 |         |     10 | 
  7934 | MILLER | CLERK     | 1300.00 |         |     10 | 
  7369 | SMITH  | CLERK     |  800.00 |         |     20 | researchmgr
  7566 | JONES  | MANAGER   | 2975.00 |         |     20 | researchmgr
  7788 | SCOTT  | ANALYST   | 3000.00 |         |     20 | researchmgr
  7876 | ADAMS  | CLERK     | 1100.00 |         |     20 | researchmgr
  7902 | FORD   | ANALYST   | 3000.00 |         |     20 | researchmgr
  7499 | ALLEN  | SALESMAN  | 1600.00 | 1200.00 |     30 | salesmgr
  7521 | WARD   | SALESMAN  | 1250.00 |  937.50 |     30 | salesmgr
  7654 | MARTIN | SALESMAN  | 1250.00 |  937.50 |     30 | salesmgr
  7698 | BLAKE  | MANAGER   | 2850.00 | 2137.50 |     30 | salesmgr
  7844 | TURNER | SALESMAN  | 1500.00 | 1125.00 |     30 | salesmgr
  7900 | JAMES  | CLERK     |  950.00 |  712.50 |     30 | salesmgr
(14 rows)
```

由于在ADD\_POLICY存储过程中将update\_check参数设为TRUE，所以下列INSERT命令会产生异常。 且由于给列authid的researchmgr值与会话用户salesmgr不匹配，所以使政策失效。

``` {#codeblock_dnh_lgx_xug}
edb=> INSERT INTO vpemp VALUES (9001,'SMITH','ANALYST',3200.00,NULL,20, 'researchmgr');
ERROR:  policy with check option violation
DETAIL:  Policy predicate was evaluated to FALSE with the updated values
```

如果我们将update\_check设为FALSE，上面描述的INSERT命令就会生效。

下列示例说明了要应用于政策的sec\_relevant\_cols参数仅在SQL命令中引用特定列时使用。下面使用于这个示例中的政策函数选择了员工薪水少于2000的记录。

``` {#codeblock_hbx_nto_udw}
CREATE OR REPLACE FUNCTION sal_lt_2000 (
    p_schema        VARCHAR2,
    p_object        VARCHAR2
)
RETURN VARCHAR2
IS
BEGIN
    RETURN 'sal < 2000';
END;
```

创建政策是为了在SELECT命令包括sal或comm列时，执行所创建的政策：

``` {#codeblock_9os_p2q_bex}
DECLARE
    v_object_schema         VARCHAR2(30) := 'public';
    v_object_name           VARCHAR2(30) := 'vpemp';
    v_policy_name           VARCHAR2(30) := 'secure_salary';
    v_function_schema       VARCHAR2(30) := 'enterprisedb';
    v_policy_function       VARCHAR2(30) := 'sal_lt_2000';
    v_statement_types       VARCHAR2(30) := 'SELECT';
    v_sec_relevant_cols     VARCHAR2(30) := 'sal,comm';
BEGIN
    DBMS_RLS.ADD_POLICY(
        v_object_schema,
        v_object_name,
        v_policy_name,
        v_function_schema,
        v_policy_function,
        v_statement_types,
        sec_relevant_cols => v_sec_relevant_cols
    );
END;
```

如果一个查询没有引用列sal 或 comm，那就是没有应用政策。下列查询返回的是表vpemp的所有14行记录：

``` {#codeblock_zjc_lh3_3lx}
edb=# SELECT empno, ename, job, deptno, authid FROM vpemp;
 empno | ename  |    job    | deptno |   authid    
-------+--------+-----------+--------+-------------
  7782 | CLARK  | MANAGER   |     10 | 
  7839 | KING   | PRESIDENT |     10 | 
  7934 | MILLER | CLERK     |     10 | 
  7369 | SMITH  | CLERK     |     20 | researchmgr
  7566 | JONES  | MANAGER   |     20 | researchmgr
  7788 | SCOTT  | ANALYST   |     20 | researchmgr
  7876 | ADAMS  | CLERK     |     20 | researchmgr
  7902 | FORD   | ANALYST   |     20 | researchmgr
  7499 | ALLEN  | SALESMAN  |     30 | salesmgr
  7521 | WARD   | SALESMAN  |     30 | salesmgr
  7654 | MARTIN | SALESMAN  |     30 | salesmgr
  7698 | BLAKE  | MANAGER   |     30 | salesmgr
  7844 | TURNER | SALESMAN  |     30 | salesmgr
  7900 | JAMES  | CLERK     |     30 | salesmgr
(14 rows)
```

如果查询引用了列sal 或 comm，那么这个查询则应用了政策。然后这个查询删除了任何sal大于或等于2 0 00的记录。如下所示：

``` {#codeblock_7on_vtf_bpn}
edb=# SELECT empno, ename, job, sal, comm, deptno, authid FROM vpemp;
 empno | ename  |   job    |   sal   |  comm   | deptno |   authid    
-------+--------+----------+---------+---------+--------+-------------
  7934 | MILLER | CLERK    | 1300.00 |         |     10 | 
  7369 | SMITH  | CLERK    |  800.00 |         |     20 | researchmgr
  7876 | ADAMS  | CLERK    | 1100.00 |         |     20 | researchmgr
  7499 | ALLEN  | SALESMAN | 1600.00 | 1200.00 |     30 | salesmgr
  7521 | WARD   | SALESMAN | 1250.00 |  937.50 |     30 | salesmgr
  7654 | MARTIN | SALESMAN | 1250.00 |  937.50 |     30 | salesmgr
  7844 | TURNER | SALESMAN | 1500.00 | 1125.00 |     30 | salesmgr
  7900 | JAMES  | CLERK    |  950.00 |  712.50 |     30 | salesmgr
(8 rows)
```

## DROP\_POLICY {#section_ghs_eg8_j9n .section}

DROP\_POLICY存储过程用于删除已有的政策。但DROP\_POLICY存储过程不能删除与政策相关的政策函数及数据库对象。

只有超级用户才能执行DROP\_POLICY存储过程。

``` {#codeblock_fhe_syv_or8}
DROP_POLICY(object_schema VARCHAR2, object_name VARCHAR2,

  policy_name VARCHAR2)
```

**参数**

|参数名称|描述|
|----|--|
|object\_schema|包含数据库对象（政策应用于此数据库对象之上）的模式名称。|
|object\_name|数据库对象（政策应用于此数据库对象之上）的名称。|
|policy\_name|要删除的政策名称。|

**示例**

下列示例删除了应用于表public. Vpemp之上的secure\_update政策：

``` {#codeblock_vo9_x9l_bl7}
DECLARE
    v_object_schema         VARCHAR2(30) := 'public';
    v_object_name           VARCHAR2(30) := 'vpemp';
    v_policy_name           VARCHAR2(30) := 'secure_update';
BEGIN
    DBMS_RLS.DROP_POLICY(
        v_object_schema,
        v_object_name,
        v_policy_name
    );
END;
```

## ENABLE\_POLICY {#section_9pb_41b_eas .section}

ENABLE\_POLICY存储过程用于启用或禁用指定数据库对象上已有的政策。

只有超级用户才能执行ENABLE\_POLICY存储过程。

``` {#codeblock_zpx_81e_mxs}
ENABLE_POLICY(object_schema VARCHAR2, object_name VARCHAR2,
  policy_name VARCHAR2, enable BOOLEAN)
```

**参数**

|参数名称|描述|
|----|--|
|object schema|包含数据库对象（政策应用于此数据库对象之上）的模式名称。|
|object name|数据库对象（政策应用于此数据库对象之上）的名称。|
|policy name|要启用或禁用的政策名称。|
|enable|当把enable设为TRUE时，政策则被启用。当设为FALSE时，政策被禁用。|

**示例**

下列示例禁用了表public .vpemp上的secure\_update政策：

``` {#codeblock_2et_jje_51j}
DECLARE
    v_object_schema         VARCHAR2(30) := 'public';
    v_object_name           VARCHAR2(30) := 'vpemp';
    v_policy_name           VARCHAR2(30) := 'secure_update';
    v_enable                BOOLEAN := FALSE;
BEGIN
    DBMS_RLS.ENABLE_POLICY(
        v_object_schema,
        v_object_name,
        v_policy_name,
        v_enable
    );
END;
```

