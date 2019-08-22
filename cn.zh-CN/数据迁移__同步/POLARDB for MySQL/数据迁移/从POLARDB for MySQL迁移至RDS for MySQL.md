# 从POLARDB for MySQL迁移至RDS for MySQL {#concept_fvw_kpf_1hb .concept}

本文介绍使用阿里云[数据传输服务（DTS）](https://www.alibabacloud.com/help/zh/product/26590.htm)，将POLARDB for MySQL迁移至RDS for MySQL的操作步骤及注意事项。

## 迁移前准备工作 {#section_zsh_m1h_1hb .section}

-   **为源集群设置IP白名单** 

    迁移前，您需要为源POLARDB集群[设置白名单](../../../../intl.zh-CN/POLARDB for MySQL快速入门/设置集群白名单.md#)，在白名单中添加DTS的IP段。

    **说明：** 您只需放开目标数据库所在区域对应的DTS IP段。本案例中，目标数据库地区为杭州，您只需要添加杭州地区的DTS IP地址段。

-   **创建数据库账号** 

    迁移任务配置时，需要提供源POLARDB集群及目的RDS实例的迁移账号。如果尚未创建迁移账号，您可以参考[POLARDB创建集群账号](intl.zh-CN/POLARDB for MySQL快速入门/创建数据库账号.md)和[RDS for MySQL创建账号](https://www.alibabacloud.com/help/zh/doc-detail/87038.htm)。先在源集群及目的实例中创建迁移账号，并将要迁移的库表的读写权限授权给上面创建的账号。


## 迁移权限要求 {#section_gmj_3tm_4gb .section}

当使用 DTS 进行**POLARDB** \> **RDS for MySQL**迁移时，不同的迁移类型，对源端和目标端数据库的迁移账号权限要求如下：

|数据库类型|结构迁移|全量数据迁移|
|-----|----|------|
|源 POLARDB 集群|只读权限|只读权限|
|目的RDS for MySQL实例|读写权限|读写权限|

## 注意事项 {#section_c2v_xfg_chb .section}

-   POLARDB暂不支持增量迁移；
-   保证迁移数据一致性，在开始迁移前，需停止写入数据到源POLARDB集群；
-   为保证迁移成功，目标实例的存储空间应大于源POLARDB集群已使用空间。

## 迁移步骤 {#section_tvx_5bh_1hb .section}

1.  登录[DTS控制台](https://dts.console.aliyun.com/)。
2.  在左侧导航栏选择**数据迁移**，然后在右上角单击**创建迁移任务**。
3.  填写源库和目标库信息，具体参数配置说明如下。

    |库类别|参数|说明|
    |---|--|--|
    |源库|实例类型|源库实例类型，选择**有公网IP的自建数据库**。|
    |实例地区|源POLARDB集群所在的地域。|
    |数据库类型|源数据库类型，选择**MySQL**。|
    |主机名或IP地址|POLARDB集群的公网集群地址。您可以参考[查看连接地址](../../../../intl.zh-CN/POLARDB for MySQL快速入门/查看连接地址.md#)。|
    |端口|默认的3306端口。|
    |数据库账号|POLARDB集群的账号。|
    |数据库密码|POLARDB集群账号的密码。|
    |目标库|实例类型|目标实例的类型，选择**RDS实例**。|
    |实例地区|目标实例的地域。|
    |RDS实例ID|目标实例的ID。|
    |数据库账号|目标实例的拥有读写权限的账号。|
    |数据库密码|目标实例的对应账号的密码。|
    |连接方式|有**非加密传输**和**SSL安全连接**两种连接方式，选择SSL安全加密连接会显著增加CPU消耗。 **说明：** 只有支持并开启了[SSL安全连接](https://www.alibabacloud.com/help/zh/doc-detail/32474.htm)的实例才需要选择SSL安全连接。

 |

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136115/156645741140347_zh-CN.png)

4.  填写完毕后单击**测试连接**，确定源库和目标库都测试通过。
5.  单击**授权白名单并进入下一步**。
6.  选择**迁移类型**和**迁移对象**。

    -   **迁移类型**：选择**结构迁移**和**全量数据迁移**。（暂不支持增量迁移。）为保证迁移数据一致性，在开始迁移前，需停止写入数据到源集群。
        -   结构迁移：

            DTS 会将迁移对象的结构定义迁移到目标实例。目前 DTS 支持结构迁移的对象包括：表。其他对象如视图、同义词、触发器、存储过程、存储函数、包、自定义类型等暂不支持。

        -   全量数据迁移：

            DTS 会将源数据库迁移对象的存量数据全部迁移到目标实例。

    -   **迁移对象**：选择要迁移的对象，单击向右的箭头，将选中的对象添加到右侧。

        **说明：** 

        -   暂时不支持对系统表的迁移。
        -   目标集群中不能有和迁移对象同名的对象。将鼠标移至右侧框中的对象，单击**编辑**按钮，即可修改迁移后的对象名。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136115/156645741140349_zh-CN.png)

7.  单击**预检查并启动**，等待预检查结束。

    **说明：** 如果检查失败，可以根据错误项的提示进行修复，然后重新启动任务。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136115/156645741140350_zh-CN.png)

8.  单击**下一步**，在**购买配置确认**对话框中，勾选**《数据传输（按量付费）服务条款》**并单击**立即购买并启动**。

    **说明：** 结构迁移和全量迁移任务暂不收费。

9.  单击目标地域，查看迁移状态。迁移完成时，状态为**已完成**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136115/156645741240351_zh-CN.png)


