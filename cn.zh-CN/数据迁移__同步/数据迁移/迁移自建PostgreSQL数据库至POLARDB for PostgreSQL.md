# 迁移自建PostgreSQL数据库至POLARDB for PostgreSQL {#concept_26607_zh .concept}

本文介绍通过`pg_dumpall`、`pg_dump`和`pg_restore`命令将自建PostgreSQL数据库迁移至POLARDB for PostgreSQL中。

迁移的源库为RDS for PostgreSQL实例时，请参考[迁移RDS for PostgreSQL数据库至POLARDB for PostgreSQL](cn.zh-CN/数据迁移__同步/数据迁移/迁移RDS for PostgreSQL数据库至POLARDB for PostgreSQL.md#)。

## 前提条件 {#section_vvx_gbt_shb .section}

POLARDB for PostgreSQL实例的存储空间应大于自建PostgreSQL数据库的存储空间。

## 注意事项 {#section_t4r_31t_shb .section}

该操作为全量数据迁移。为避免迁移前后数据不一致，迁移操作开始前请停止自建数据库的相关业务，并停止数据写入。

## 准备工作 {#section_bx1_51t_shb .section}

1.  创建一个Linux操作系统的ECS实例，本案例使用的ECS为Ubuntu 16.04 64位操作系统。详情请参考[创建ECS实例](https://help.aliyun.com/document_detail/25424.html)。

    **说明：** 

    -   要求ECS实例和迁移的目标POLARDB for PostgreSQL实例处于同一个专有网络。
    -   可创建一个按量付费的ECS实例，迁移完成后释放实例。
2.  在ECS实例中安装PostgreSQL，以便执行数据恢复的命令。详情请参考[PostgreSQL官方文档](https://www.postgresql.org/docs/11/installation.html)。

    **说明：** 请确保安装的PostgreSQL数据库版本与自建PostgreSQL数据库版本一致。


## 操作步骤一 备份自建数据库 {#section_rsp_q1s_shb .section}

该操作为全量数据迁移。为避免迁移前后数据不一致，迁移操作开始前请停止自建数据库的相关业务，并停止数据写入。

1.  在自建PostgreSQL数据库服务器上执行以下命令，备份数据库中的所有角色信息。

    ```
    pg_dumpall -U <username> -h <hostname> -p <port> -r -f <filename>
    ```

    参数说明：

    -   <username\>：登录自建PostgreSQL数据库的账号。
    -   <hostname\>：自建PostgreSQL数据库的连接地址，本机可使用localhost。
    -   <port\>：数据库服务的端口号。
    -   <filename\>：生成的备份文件名称。
    示例：

    ```
    pg_dumpall -U postgres -h localhost -p 5432 -r -f roleinfo.sql
    ```

2.  命令行提示`Password:`时，输入数据库账号对应的密码，开始备份数据库中的所有角色信息。
3.  使用`vim`命令将角色信息备份文件中的`SUPERUSER`替换为`polar_superuser`。

    **说明：** 如果角色信息备份文件中没有`SUPERUSER`信息，可跳过本步骤。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/218250/155841538647244_zh-CN.png)

4.  在自建PostgreSQL数据库服务器上执行以下命令，备份数据库中的数据。

    ```
    pg_dump -U <username> -h <hostname> -p <port> <dbname> -Fd -j <njobs> -f <dumpdir>
    ```

    参数说明：

    -   <username\>：登录自建PostgreSQL数据库的账号。
    -   <hostname\>：自建PostgreSQL数据库的连接地址，本机可使用localhost。
    -   <port\>：数据库服务的端口号。
    -   <dbname\>：要备份的数据库名。
    -   <njobs\>：同时执行备份作业的并发数。

        **说明：** 

        -   参数<njobs\>可减少转储的时间，但也会增加数据库服务器的负载。
        -   如果您的自建PostgreSQL数据库是9.2以前的版本，您还需要指定`--no-synchronized-snapshots`参数。
    -   <dumpdir\>：生成的备份文件所属目录。
    示例：

    ```
    pg_dump -U postgres -h localhost -p 5432 mytestdata -Fd -j 5 -f postgresdump
    ```

5.  命令行提示`Password:`时，输入数据库账号对应的密码，数据库开始备份。
6.  等待备份完成，PostgreSQL数据库数据将备份至指定的目录中，本案例为postgresdump。

## 操作步骤二 数据迁移至POLARDB for PostgreSQL {#section_pky_xxs_shb .section}

1.  将备份文件所属的目录上传至ECS实例中。

    **说明：** 包含角色信息备份文件和数据库备份文件。

2.  在ECS上执行以下命令，将角色信息备份文件中的角色信息迁移至POLARDB for PostgreSQL实例中。

    ```
    psql -U <username> -h <hostname>  -p <port> -d <dbname>  -f <filename>
    ```

    参数说明：

    -   <username\>：登录POLARDB for PostgreSQL数据库的账号。
    -   <hostname\>：POLARDB for PostgreSQL实例的主地址（私网）。
    -   <port\>：数据库服务的端口号，默认为**1921**。
    -   <dbname\>：连接的数据库的名称，默认为postgres。
    -   <filename\>：角色信息备份文件名。
    ```
    psql -U gctest -h pc-xxxxxxxx.pg.polardb.cn-qd-pldb1.rds.aliyuncs.com -d postgres -p 1921 -f roleinfo.sql
    ```

3.  命令行提示`Password:`时，输入数据库账号对应的密码，角色信息开始导入。
4.  在ECS上执行以下命令，将数据库数据恢复至POLARDB for PostgreSQL实例中。

    ```
    pg_restore -U <username> -h <hostname> -p <port> -d <dbname> -j <njobs> <dumpdir>
    ```

    参数说明：

    -   <username\>：登录POLARDB for PostgreSQL数据库的账号。
    -   <hostname\>：POLARDB for PostgreSQL实例的主地址（私网），详情请参考[查看连接地址](../../../../cn.zh-CN/POLARDB for PostgreSQL快速入门/连接数据库集群/查看连接地址.md#)。
    -   <port\>：数据库服务的端口号，默认为**1921**。
    -   <dbname\>：连接并直接恢复到的目标数据库名。

        **说明：** 目标数据库需已存在，如不存在请在目标实例中创建该数据库。

    -   <njobs\>：同时执行数据恢复作业的并发数。

        **说明：** 此选项可减少数据恢复的时间，但也会增加数据库服务器的负载。

    -   <dumpdir\>：备份文件所在目录。
    示例：

    ```
    pg_restore -U gctest -h pc-mxxxxxxxx.pg.polardb.cn-qd-pldb1.rds.aliyuncs.com -p 1921 -d mytestdata -j 6 postgresdump
    ```

5.  命令行提示 `Password:`时，输入数据库账号对应的密码，数据开始迁移。

    **说明：** 如果忘记密码，请参考[重置数据库账号的密码](../../../../cn.zh-CN/POLARDB for PostgreSQL用户指南/账号管理/管理数据库账号.md#section_ckb_hpq_tdb)。


等待数据迁移完成即可。

