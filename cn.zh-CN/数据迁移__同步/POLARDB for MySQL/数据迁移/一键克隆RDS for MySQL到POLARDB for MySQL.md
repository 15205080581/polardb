# 一键克隆RDS for MySQL到POLARDB for MySQL {#task_1580301 .task}

POLARDB支持从RDS for MySQL一键克隆数据到新的POLARDB for MySQL集群。

-   克隆只能在相同地域内进行。
-   源RDS实例版本为RDS for MySQL 5.6高可用版。
-   源RDS实例未开启[TDE](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置透明数据加密.md#)和[SSL](../../../../cn.zh-CN/RDS for MySQL 用户指南/数据安全性/设置 SSL 加密.md#)。
-   源RDS实例的表存储引擎为InnoDB。
-   如果RDS处于高安全模式（数据库代理模式），需要创建有高权限账号，或者切换到高性能模式，才能进行一键克隆。

POLARDB是阿里云自研的下一代关系型云数据库，主要优势如下：

-   存储容量高：最高可达100TB。
-   性能高：最高可以提升至MySQL的6倍。
-   Serverless存储：存储容量无需提前购买，自动扩缩容，按使用量计费。
-   临时升配：临时升级规格，轻松应对短期的业务高峰。

详情请参见[产品优势](../../../../cn.zh-CN/产品简介/产品优势.md#)。

一键克隆功能将会新建一个与源RDS实例的数据相同的POLARDB集群，POLARDB集群包含源RDS实例的账号、数据库、IP白名单和必要的参数。源RDS实例的增量数据不会同步到POLARDB集群。

**说明：** 如果需要在新建POLARDB集群的同时，使源RDS实例的增量数据实时同步到POLARDB集群，即实现平滑迁移（不停机迁移），请参见[一键升级RDS for MySQL到POLARDB for MySQL](cn.zh-CN/数据迁移__同步/POLARDB for MySQL/数据迁移/一键升级RDS for MySQL到POLARDB for MySQL.md#)。

## 一键克隆的功能亮点 {#section_z2a_olf_h1c .section}

-   免费
-   克隆过程数据0丢失

## 一键克隆的操作步骤 {#section_usc_hx6_upb .section}

1.  登录[POLARDB控制台](https://polardb.console.aliyun.com)。
2.  单击**创建新集群**。
3.  选择包年包月或按小时付费页签。
4.  设置参数，请参见[参数说明](#section_08l_pug_70k)
5.  设置**购买时长**（仅针对包年包月集群），然后单击右侧的**立即购买**。
6.  确认订单信息，阅读和勾选**服务协议**，单击**去开通**。

## 参数说明 {#section_08l_pug_70k .section}

|参数|说明|
|--|--|
|**地域**|源RDS for MySQL实例所在地域。 **说明：** 克隆的POLARDB集群也在此地域。

 |
|**创建方式**|集群的创建方式： -   **默认创建**：创建一个全新的POLARDB集群。
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

## 常见问题 {#section_3l3_e5l_u2i .section}

**从RDS克隆**会影响源RDS实例吗？

答：不会影响源RDS实例的正常运行。

## 相关API {#section_nj0_s59_1jn .section}

|API|描述|
|---|--|
|[CreateDBCluster](../../../../cn.zh-CN/API参考/集群管理/CreateDBCluster.md#)|创建POLARDB集群。 **说明：** 一键克隆时，参数**CreationOption**取值需要为**CloneFromRDS**。

 |

请尽快将应用的数据库连接地址修改为POLARDB的地址，详情请参见[查看连接地址](../../../../cn.zh-CN/POLARDB for MySQL快速入门/查看连接地址.md#)。

