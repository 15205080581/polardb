# SQL调优 {#concept_l1d_pyr_2gb .concept}

SQL调优功能可以根据您输入的SQL语句，提出优化建议。您也可以直接在SQL调优功能中登录数据库，并使用SQL命令进行插入和管理数据的操作。本文将介绍如何使用SQL调优功能优化和执行SQL语句。

## 操作步骤 {#section_zj3_yxk_xfb .section}

1.  进入[POLARDB控制台](https://polardb.console.aliyun.com/)。
2.  选择地域。
3.  找到目标集群，单击集群名称列的**集群ID**。
4.  在左侧导航栏中选择**诊断与优化** \> **问题分析**。
5.  选择SQL调优页签，单击右侧**登录数据库**。
6.  填写登录信息后单击**登录**。

    |参数名称|说明|
    |----|--|
    |用户名|有管理相应数据库权限的账号名称。|
    |密码|登录数据库的账号对应的密码。|

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81403/155747464434823_zh-CN.png)

7.  选择要查询或管理的数据库。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81403/155747464434824_zh-CN.png)

8.  在输入框中填写SQL语句，然后选择如下操作。

    **说明：** SQL操作中提供的所有功能都不支持批量操作，若您同时输入了多条SQL语句，只能选中一条目标语句，进行后续操作。

    -   单击**查看执行计划**，即可在执行结果中查看SQL语句具体的执行计划。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81403/155747464434818_zh-CN.png)

    -   单击**智能诊断**，系统会对所输入的SQL语句进行诊断并给出优化建议，如索引优化。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81403/155747464434819_zh-CN.png)

    -   单击**执行语句**并在弹出的对话框中单击**确认**，即可在已选数据库中执行SQL命令，可在执行结果中查看SQL执行结果。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81403/155747464434820_zh-CN.png)

    -   单击**格式优化**，系统会自动优化所输入SQL语句的格式。
    -   单击**撤销**，可以撤销上一步对SQL语句进行的修改。若您误撤销了上一步的操作，可以立刻单击**重做**，即可恢复被撤销的修改。

