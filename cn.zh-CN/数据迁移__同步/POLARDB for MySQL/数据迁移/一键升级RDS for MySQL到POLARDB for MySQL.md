# 一键升级RDS for MySQL到POLARDB for MySQL {#concept_593020 .concept}

POLARDB支持将RDS for MySQL一键升级为POLARDB for MySQL。

## POLARDB简介 {#section_hom_hgv_q2a .section}

POLARDB是阿里云自研的下一代关系型云数据库，主要优势如下：

-   存储容量高：最高可达100TB。
-   性能高：最高可以提升至MySQL的6倍。
-   Serverless存储：存储容量无需提前购买，自动扩缩容，按使用量计费。
-   临时升配：临时升级规格，轻松应对短期的业务高峰。

详情请参见[产品优势](../cn.zh-CN/产品简介/产品优势.md#)。

## 一键升级的功能亮点 {#section_4ty_tix_1xp .section}

-   迁移完全免费。
-   迁移过程数据0丢失。
-   支持增量迁移，停机时间小于10分钟。
-   支持回滚，迁移失败可以在10分钟内恢复。

## 迁移流程 {#section_aoh_yoz_8jt .section}

1.  参考[从RDS迁移](#)的说明，创建一个与源RDS实例数据相同的POLARDB集群，源RDS实例的增量数据会实时同步到该POLARDB集群。

    **说明：** 需要在7天内修改应用端的数据库地址为POLARDB地址，确认业务正常，以及单击**完成迁移**。单击**完成迁移**会中断RDS和POLARDB之间的数据同步。

2.  单击**迁移切换**。该操作将源RDS实例修改为只读，将POLARDB集群修改为可读可写，POLARDB的增量数据会实时同步到RDS。修改数据库连接地址。

    具体操作请参见[迁移切换](#)。

    **说明：** 迁移切换后，也可以选择[迁移回滚](#)。

3.  [完成迁移](#)。

## 注意事项 {#section_ldl_wsn_13b .section}

-   迁移只能在相同地域内进行。
-   POLARDB集群包含源RDS实例的账号、数据库、IP白名单和必要的参数。
-   源RDS实例在迁移时不能修改参数。

## 前提条件 {#section_ezw_wsn_13b .section}

-   源RDS实例版本为RDS for MySQL 5.6高可用版。
-   源RDS实例未开启[TDE](../../../../../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置透明数据加密.md#)和[SSL](../../../../../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置 SSL 加密.md#)。
-   源RDS实例的表存储引擎为InnoDB。

## 从RDS迁移 {#section_s4t_zsn_13b .section}

本操作将创建一个与源RDS实例数据相同的POLARDB集群，源RDS实例的增量数据会实时同步到该POLARDB集群。

1.  您可以使用如下两种方式进入创建新集群的页面：
    -   1.  登录[POLARDB控制台](https://polardb.console.aliyun.com)。
2.  单击**创建新集群**。
    -   1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)
2.  在页面左上角，选择实例所在的地域。
3.  找到[符合条件](#section_ezw_wsn_13b)的源RDS实例，单击实例ID。
4.  在上方单击**升级为POLARDB**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156506925951092_zh-CN.png)

2.  选择包年包月或按小时付费页签。
3.  设置以下参数。

    |参数|说明|
    |--|--|
    |**地域**|源RDS for MySQL实例所在地域。 **说明：** 新建的POLARDB集群也在此地域。

 |
    |**创建方式**|选择**从RDS迁移**。     -   **默认创建**：创建一个全新的POLARDB集群。
    -   **从RDS克隆**：基于所选的RDS实例，克隆一个数据完全一样的POLARDB集群。
    -   **从RDS迁移**：从RDS实例克隆一个POLARDB集群，同时保持数据同步。默认开启新集群的Binlog。
 |
    |**源RDS引擎**|源RDS实例的引擎类型，不可变更。|
    |**源RDS版本**|源RDS实例的版本，不可变更。|
    |**源RDS实例**|可选的源RDS实例，不包括只读实例。|
    |**可用区**| 可用区是地域中的一个独立物理区域，不同可用区之间没有实质性区别。

 您可以选择将POLARDB集群与ECS创建在同一可用区或不同的可用区。

 |
    |**网络类型**|POLARDB集群的网络类型，不可变更。|
    |**VPC网络** **VPC交换机**

 |POLARDB集群所属的VPC和虚拟交换机。请确保POLARDB集群与需要连接的ECS创建于同一个VPC，否则它们无法通过内网互通，无法发挥最佳性能。|
    |**数据库引擎**|POLARDB集群的数据库引擎，不可变更。|
    |**节点规格**|按需选择，建议不低于源RDS实例规格。所有POLARDB节点均为独享型，性能稳定可靠。详情请参见[规格与定价](../cn.zh-CN/产品定价/规格与定价.md#)。|
    |**节点个数**|无需选择。系统将自动创建一个与主节点规格相同的只读节点。|
    |**存储费用**|无需选择容量，根据实际数据使用量按小时计费。详情请参见[规格与定价](../cn.zh-CN/产品定价/规格与定价.md#)。|
    |**集群名称**|填写集群名称用于区分业务用途。如果留空，系统将自动生成一个集群名称。创建集群后还可以修改。|

4.  设置**购买时长**（仅针对包年包月集群），然后单击右侧的**立即购买**。
5.  确认订单信息，阅读和勾选**服务协议**，单击**去开通**，完成支付。
6.  进入[POLARDB控制台](https://polardb.console.aliyun.com)，查看新建的POLARDB集群的状态。

    **说明：** 

    -   集群创建后开始从RDS实例同步数据，7 天内需要完成修改数据库连接地址以及[完成迁移](#)操作。超过7天将自动关闭迁移功能。
    -   您可以在此步骤选择取消迁移，相关影响请参见[迁移常见问题](#)。

## 迁移切换 {#section_jdh_0d3_zjz .section}

**前提条件**

-   已完成[从RDS迁移](#section_s4t_zsn_13b)的操作。
-   **复制延迟**小于60秒。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156506925951400_zh-CN.png)


**操作步骤**

满足前提条件后，您可以进行迁移切换，然后修改应用里的数据库连接地址。

1.  进入[POLARDB控制台](https://polardb.console.aliyun.com)。
2.  找到目标集群，单击集群的ID。
3.  在基本信息页面单击**迁移切换**，在弹出的对话框中单击**确定**。

    本操作将源RDS实例修改为只读，将POLARDB集群修改为可读可写，同时会将POLARDB集群的新增数据同步到RDS实例。

    **说明：** 

    -   数据同步的延迟超过60秒时无法进行迁移切换。
    -   切换过程一般小于5分钟。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156506926051031_zh-CN.png)

4.  刷新页面，当**POLARDB读写状态**显示为**读写**后，尽快修改应用里的数据库连接地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156506926051038_zh-CN.png)

    **说明：** 迁移切换完成后，也可以选择[迁移回滚](#)。


## 完成迁移 {#section_3ds_ojf_lmm .section}

[从RDS迁移](#section_s4t_zsn_13b)后，需要在7天内修改数据库连接地址以及单击**完成迁移**。该操作将中断POLARDB集群和RDS实例间的数据同步。

**警告：** 由于本操作将中断POLARDB集群和RDS实例间的数据同步，不再提供[迁移回滚](#)功能，建议您使用一段时间POLARDB集群，确认正常后再执行本操作。

1.  进入[POLARDB控制台](https://polardb.console.aliyun.com)。
2.  找到目标集群，单击集群的ID。
3.  在基本信息页面，单击**完成迁移**，在弹出的对话框中单击**确定**。

    **说明：** 

    -   单击**确定**后，系统将在约2分钟内中断同步关系，期间**完成迁移**按钮不会消失，请勿重复点击。
    -   您可以选择是否关闭POLARDB集群的Binlog。关闭Binlog会带来少量的写入性能提升，但需要重启POLARDB。
    ![完成迁移](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156506926048987_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156506926051039_zh-CN.png)

4.  如果不再需要源RDS实例，可以释放实例。

## 迁移回滚 {#section_hw4_hy4_13b .section}

迁移切换完成后，您也可以进行回滚（RDS实例为可读可写，POLARDB集群为只读，同时会将RDS实例的数据同步到POLARDB集群）。详细操作步骤如下：

1.  进入[POLARDB控制台](https://polardb.console.aliyun.com)。
2.  找到目标集群，单击集群的ID。
3.  在基本信息页面单击**迁移回滚**，在弹出的对话框中单击**确定**。

    **说明：** 单击**确定**后RDS实例为可读可写，POLARDB集群为只读，同时会将RDS实例的数据同步到POLARDB集群。当**源RDS读写状态**显示为**读写**后，请尽快修改应用里的数据库连接地址为RDS连接地址。

    ![迁移回滚](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156506926048988_zh-CN.png)


## 迁移常见问题 {#section_lxr_3fp_13b .section}

-   **从RDS迁移**会影响源RDS实例吗？

    答：不会影响源RDS实例的正常运行。

-   平滑迁移对业务有影响吗？

    答：平滑迁移能够保证迁移过程不丢失数据，停机时间小于10分钟，如果有需要还可以进行回滚。

-   取消迁移会有什么影响？

    答：取消迁移后，源RDS实例可以修改参数；POLARDB集群恢复可读可写，且数据不会释放。手动取消时可以选择是否关闭POLARDB集群的Binlog，自动取消时不会关闭。


## 相关API {#section_yny_y59_23u .section}

|API|描述|
|---|--|
|[CreateDBCluster](../cn.zh-CN/API参考/集群管理/CreateDBCluster.md#)|创建POLARDB集群。 **说明：** 一键升级时，参数**CreationOption**取值需要为**MigrationFromRDS**。

 |
|[DescribeDBClusterMigration](../cn.zh-CN/API参考/从RDS迁移/DescribeDBClusterMigration.md#)|查询POLARDB集群的迁移状态。|
|[ModifyDBClusterMigration](../cn.zh-CN/API参考/从RDS迁移/ModifyDBClusterMigration.md#)|修改迁移任务，进行任务的切换或回滚。|
|[CloseDBClusterMigration](../cn.zh-CN/API参考/从RDS迁移/CloseDBClusterMigration.md#)|取消或完成迁移。|

