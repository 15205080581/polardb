# 一键克隆RDS for MySQL到POLARDB for MySQL {#concept_627560 .concept}

POLARDB支持从RDS for MySQL一键克隆数据到新的POLARDB for MySQL集群。

## 功能亮点 {#section_z2a_olf_h1c .section}

-   免费；
-   迁移过程数据0丢失；
-   迁移宕机时间小于10分钟；
-   支持回滚（迁移失败可以在10分钟内回滚）。

## 功能概述 {#section_xly_94v_79y .section}

在创建POLARDB集群时，除了创建[全新的POLARDB集群](../../../../cn.zh-CN/POLARDB for MySQL快速入门/创建POLARDB for MySQL数据库集群.md#)，阿里云还提供如下两种方式：

-   [从RDS克隆](cn.zh-CN/POLARDB for MySQL用户指南/数据迁移__同步/数据迁移/一键克隆RDS for MySQL到POLARDB for MySQL.md#)：从RDS备份文件恢复全量数据到POLARDB新集群上，新集群创建后，两者完全独立，互不影响。

    **说明：** **从RDS克隆**通常用于迁移前进行测试、验证等。

-   [从RDS迁移](cn.zh-CN/POLARDB for MySQL用户指南/数据迁移__同步/数据迁移/一键升级RDS for MySQL到POLARDB for MySQL.md#)：从RDS备份文件恢复全量数据到POLARDB新集群，然后利用源RDS实例的Binlog单向同步数据到POLARDB集群。平滑迁移过程中，阿里云提供[迁移回滚](cn.zh-CN/POLARDB for MySQL用户指南/数据迁移__同步/数据迁移/一键升级RDS for MySQL到POLARDB for MySQL.md#section_hw4_hy4_13b)功能，您可以放心迁移。

**从RDS迁移**是在**从RDS克隆**的基础上增加了单向数据同步，保证POLARDB集群的数据和源RDS实例相同，便于后续进行业务切换。对比示意图如下。

![对比示意图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475602/156049913949076_zh-CN.png)

## 注意事项 {#section_c9r_z0e_eiq .section}

-   克隆只能在相同地域内进行。
-   POLARDB集群包含源RDS实例的账号、数据库、IP白名单和必要的参数。

## 前提条件 {#section_o3x_p6s_u0l .section}

-   源RDS实例版本为RDS for MySQL 5.6高可用版。
-   源RDS实例未开启[TDE](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置透明数据加密.md#)和[SSL](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置 SSL 加密.md#)。
-   源RDS实例的表存储引擎为InnoDB。

## 操作步骤 {#section_usc_hx6_upb .section}

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
    -   **从RDS迁移**：先从RDS实例克隆一个POLARDB集群，同时保持同步。默认开启新集群的Binlog。
 这里选择**从RDS克隆**。

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

## 常见问题 {#section_3l3_e5l_u2i .section}

**从RDS克隆**会影响源RDS实例吗？

答：不会影响源RDS实例的正常运行。

