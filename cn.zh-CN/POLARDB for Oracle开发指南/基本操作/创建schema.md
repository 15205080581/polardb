# 创建schema {#concept_188840 .concept}

定义一个新的模式。

## 语法 {#section_ytt_qyx_jjd .section}

``` {#codeblock_n61_y4v_rie}
CREATE SCHEMA AUTHORIZATION username schema_element [ ... ];
```

## 参数 {#section_u06_k2p_grf .section}

|参数名称|描述|
|----|--|
|username|拥有新创建模式的用户名。 模式名称与用户名相同。

 **说明：** 

-   仅限超级用户可以创建其他用户所拥有的模式。
-   在 POLARDB for Oracle中，角色、用户名必须已经存在，但是模式名称不是必须存在。
-   在Oracle中，同于模式的用户必须存在。

 |
|schema\_element|用于在模式中定义要创建对象的SQL语句。 在CREATE SCHEMA中，CREATE TABLE，CREATE VIEW, 和GRANT都可以作为子句来使用。在模式创建完后，可以使用单独的命令创建其他类型的对象 。

 |

## 描述 {#section_t1z_47o_zd6 .section}

这是CREATE SCHEMA命令的一种用法，用于创建一个新的模式，由命令中参数username所指的用户拥有。在模式中可以存放一个或多个对象。模式和对象在一个单独事务中创建，如果执行成功，所有对象都会创建成功，否则包含模式在内这些对象都不会创建。

一个模式实际上是一个命名空间：它包含命名的对象（包括表，视图等），这些对象的名称可以与其他模式下的对象名称相同。我们既可以把模式名称做为前缀来限定对象名称，以这种方式来访问对象，也可以通过设置包含所需要模式的搜索路径来访问对象。非限定的对象是在当前模式下创建的（在搜索路径前面的模式可以由函数CURRENT\_SCHEMA来确认，搜索路径和函数CURRENT\_SCHEMA不属于Oracle兼容特性）。

CREATE SCHEMA命令中包括子命令，用于在模式中创建对象。这些子命令的执行方式实际上和执行完创建模式命令后，单独执行这些子命令一样。所有创建的对象都是为指定用户所拥有。

**说明：** 创建一个模式，所涉及的用户在数据库中必须有CREATE权限。

## 示例 {#section_h46_17f_bq6 .section}

``` {#codeblock_uo2_byv_cbd}
CREATE SCHEMA AUTHORIZATION enterprisedb
    CREATE TABLE empjobs (ename VARCHAR2(10), job VARCHAR2(9))
    CREATE VIEW managers AS SELECT ename FROM empjobs WHERE job = 'MANAGER'
    GRANT SELECT ON managers TO PUBLIC;
```

