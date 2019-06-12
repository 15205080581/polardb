# RDS for MySQL平滑迁移到POLARDB for MySQL {#concept_593020 .concept}

POLARDB支持将RDS for MySQL平滑迁移到POLARDB for MySQL。

## 从RDS克隆/迁移概述 {#section_bxt_vsn_13b .section}

在创建POLARDB集群时，除了创建[全新的POLARDB集群](../../../../cn.zh-CN/POLARDB for MySQL快速入门/创建POLARDB for MySQL数据库集群.md#)，阿里云还提供如下两种方式：

-   [从RDS克隆](cn.zh-CN/POLARDB for MySQL用户指南/数据迁移__同步/数据迁移/RDS for MySQL通过克隆方式迁移到POLARDB for MySQL.md#)：从RDS备份文件恢复全量数据到POLARDB新集群上，新集群创建后，两者完全独立，互不影响。

    **说明：** **从RDS克隆**通常用于迁移前进行测试、验证等。

-   [从RDS迁移](#)：从RDS备份文件恢复全量数据到POLARDB新集群，然后利用源RDS实例的Binlog单向同步数据到POLARDB集群。平滑迁移过程中，阿里云提供[迁移回滚](#)功能，您可以放心迁移。

**从RDS迁移**是在**从RDS克隆**的基础上增加了单向数据同步，保证POLARDB集群的数据和源RDS实例相同，便于后续进行业务切换。对比示意图如下。

![对比示意图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156033331449076_zh-CN.png)

## 平滑迁移介绍 {#section_aoh_yoz_8jt .section}

RDS for MySQL平滑迁移到POLARDB for MySQL，分为如下几个步骤：

1.  创建POLARDB集群，创建时选择**从RDS迁移**，保证POLARDB集群数据和源RDS实例相同。由于是单向同步，为了保证数据正确性，RDS实例为可读可写，POLARDB集群为只读。详情请参见[从RDS迁移](#)。
2.  进行迁移切换，将RDS实例修改为只读，POLARDB集群修改为可读可写，同时利用POLARDB集群的Binlog单向同步数据到源RDS实例，为可能的[迁移回滚](#)提供保障。详情请参见[迁移切换](#)。
3.  确认业务正常后，可以执行完成迁移的操作，中断POLARDB集群和RDS实例的数据同步。详情请参见[完成迁移](#)。

详细的流程示意图如下。

![迁移流程示意图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156033331449080_zh-CN.png)

## 注意事项 {#section_ldl_wsn_13b .section}

-   迁移只能在相同地域内进行。
-   POLARDB集群包含源RDS实例的账号、数据库、IP白名单和必要的参数。
-   源RDS实例在迁移时不能修改参数。

## 前提条件 {#section_ezw_wsn_13b .section}

-   源RDS实例版本为RDS for MySQL 5.6高可用版。
-   源RDS实例未开启[TDE](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置透明数据加密.md#)和[SSL](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置 SSL 加密.md#)。

## 从RDS迁移 {#section_s4t_zsn_13b .section}

1.  进入[POLARDB控制台](https://polardb.console.aliyun.com)。
2.  单击**创建新集群**。
3.  选择包年包月或按小时付费页签。
4.  设置以下参数。

    |参数|说明|
    |--|--|
    |**地域**|源RDS for MySQL实例所在地域。 **说明：** 克隆的POLARDB集群也在此地域。

 |
    |**创建方式**|集群的创建方式：     -   **默认创建**：创建一个全新的POLARDB集群。
    -   **从RDS克隆**：基于所选的RDS实例，克隆一个数据完全一样的POLARDB集群。
    -   **从RDS迁移**：先从RDS实例克隆一个POLARDB集群，同时保持数据同步。默认开启新集群的Binlog。
 这里选择**从RDS迁移**。

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
    |**节点规格**|按需选择，建议不低于源RDS实例规格。所有POLARDB节点均为独享型，性能稳定可靠。详情请参见[规格与定价](../../../../cn.zh-CN/产品定价/规格与定价.md#)。|
    |**节点个数**|无需选择。系统将自动创建一个与主节点规格相同的只读节点。|
    |**存储费用**|无需选择容量，根据实际数据使用量按小时计费。详情请参见[规格与定价](../../../../cn.zh-CN/产品定价/规格与定价.md#)。|
    |**集群名称**|填写集群名称用于区分业务用途。如果留空，系统将自动生成一个集群名称。创建集群后还可以修改。|

5.  设置**购买时长**（仅针对包年包月集群），然后单击右侧的**立即购买**。
6.  确认订单信息，阅读和勾选**服务协议**，单击**去开通**。

## 迁移切换 {#section_jdh_0d3_zjz .section}

**从RDS迁移**之后，您可以进行迁移切换，然后修改应用里的数据库连接地址。

1.  进入[POLARDB控制台](https://polardb.console.aliyun.com)。
2.  找到目标集群，单击集群的ID。
3.  在基本信息页面单击**迁移切换**，在弹出的对话框中单击**确定**。

    **说明：** 

    -   当**POLARDB读写状态**显示为**读写**后，请尽快修改应用里的数据库连接地址。
    -   单击**确定**后RDS实例为只读，POLARDB集群为可读可写，同时会将POLARDB集群的数据同步到RDS实例。
    -   数据同步的延迟超过180秒时无法进行迁移切换。
    -   迁移切换需要在7天内完成，超过7天将自动关闭迁移功能，源RDS实例和目的POLARDB集群将恢复可读可写状态。
    -   您可以在此步骤选择取消迁移，相关影响请参见[迁移常见问题](#)。
    ![迁移切换](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156033331548986_zh-CN.png)


## 完成迁移 {#section_3ds_ojf_lmm .section}

修改应用里的数据库连接地址后，您可以完成迁移，中断POLARDB集群和RDS实例的数据同步。

**警告：** 由于本操作将中断POLARDB集群和RDS实例的数据同步，不再提供迁移回滚功能，建议您使用一段时间POLARDB集群，确认正常后再执行本操作。

1.  进入[POLARDB控制台](https://polardb.console.aliyun.com)。
2.  找到目标集群，单击集群的ID。
3.  在基本信息页面单击**完成迁移**，在弹出的对话框中单击**确定**。

    **说明：** 

    -   单击**确定**后将中断POLARDB集群和RDS实例的数据同步，不再提供迁移切换功能，相关限制也会取消。
    -   您可以选择是否关闭POLARDB集群的Binlog。为了节省费用，源RDS实例如果没有其他业务需求可以，如果是包年包月实例，需要提交工单处理。
    -   您可以在此步骤选择[迁移回滚](#)，再次交换RDS实例和POLARDB集群的读写状态。
    ![完成迁移](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156033331548987_zh-CN.png)


## 迁移回滚 {#section_hw4_hy4_13b .section}

迁移切换完成后，您也可以进行回滚（仅回滚源RDS实例和POLARDB集群的读写状态和同步数据方向，数据不会回滚）。详细操作步骤如下：

1.  进入[POLARDB控制台](https://polardb.console.aliyun.com)。
2.  找到目标集群，单击集群的ID。
3.  在基本信息页面单击**迁移回滚**，在弹出的对话框中单击**确定**。

    **说明：** 单击**确定**后RDS实例为可读可写，POLARDB集群为只读，同时会将RDS实例的数据同步到POLARDB集群。当**源RDS读写状态**显示为**读写**后，请尽快修改应用里的数据库连接地址。

    ![迁移回滚](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156033331548988_zh-CN.png)


## 迁移常见问题 {#section_lxr_3fp_13b .section}

-   **从RDS迁移**会影响源RDS实例吗？

    答：不会影响源RDS实例的正常运行。

-   平滑迁移对业务有影响吗？

    答：平滑迁移能够保证迁移过程不丢失数据，停机时间小于10分钟，如果有需要还可以进行回滚。

-   取消迁移会有什么影响？

    答：取消迁移后，源RDS实例可以修改参数；POLARDB集群恢复可读可写，且数据不会释放。手动取消时可以选择是否关闭POLARDB集群的Binlog，自动取消时不会关闭。


