# 创建POLARDB for MySQL数据库集群 {#task_1580301 .task}

本文介绍如何通过POLARDB管理控制台创建POLARDB for MySQL数据库集群。

已注册阿里云账号或已创建子账号。

-   如要注册阿里云账号，请[点此注册](https://account.alibabacloud.com/register/intl_register.htm)。
-   如要创建子账号，请参见[创建和使用子账号](intl.zh-CN/POLARDB for MySQL用户指南/账号管理/创建和使用子账号.md#)进行子账号的创建和授权。

一个集群包含一个主节点以及最多15个只读节点（最少一个，用于提供Active-Active高可用）。节点是虚拟化的数据库服务器，节点中可以创建和管理多个数据库。

**说明：** 

-   POLARDB仅支持专有网络VPC（Virtual Private Cloud）。VPC是阿里云上一种隔离的网络环境，安全性比传统的经典网络更高。

-   POLARDB与其他阿里云产品通过内网互通时才能发挥POLARDB的最佳性能，因此，建议将POLARDB与云服务器ECS配合使用，且与ECS创建于同一个VPC，否则POLARDB无法发挥最佳性能。如果您ECS的网络类型为经典网络，需将ECS从经典网络迁移到VPC。

## 操作步骤 {#section_drs_p4r_b3b .section}

1.  登录阿里云。 
    -   如果使用阿里云账号，请[点此登录](https://account.alibabacloud.com/login/login.htm)。
    -   如果使用子账号，请[点此登录](https://account.alibabacloud.com/login/login.htm)。更多信息请参见[登录子账号](intl.zh-CN/POLARDB for MySQL用户指南/账号管理/创建和使用子账号.md#section_zb2_54q_tdb)。
2.  进入[POLARDB购买页面](https://common-buy.aliyun.com/?commodityCode=polardb_sub&regionId=cn-hangzhou)。
3.  选择包年包月或按量付费。 

    **说明：** 

    -   **包年包月**：在创建集群时支付计算节点（一个主节点和一个只读节点）的费用，而存储空间会根据实际数据量按小时计费，并从账户中按小时扣除。如果您要长期使用该集群，**包年包月**方式更加划算，而且购买时长越长，折扣越多。
    -   **按量付费（按小时付费）**：无需预先支付费用，计算节点和存储空间（根据实际数据量）均按小时计费，并从账户中按小时扣除。如果您只需短期使用该集群，可以选择**按量付费**，用完即可释放，节省费用。
4.  设置如下参数。 

    |控制台区域|参数|说明|
    |:----|:-|:-|
    |基本配置|地域|集群所在的地理位置。购买后无法更换地域。 **说明：** 请确保POLARDB与需要连接的ECS创建于同一个地域，否则它们无法通过内网互通，只能通过外网互通，无法发挥最佳性能。

 |
    |创建方式|创建POLARDB集群的方式。     -   默认创建：创建一个全新的POLARDB。
    -   从RDS克隆：基于所选的RDS实例，快速克隆一个数据完全一样的POLARDB集群。详情请参见[../DNPOLARDB19100108/ZH-CN\_TP\_505489\_V14.dita\#task\_1580301](../DNPOLARDB19100108/ZH-CN_TP_505489_V14.dita#task_1580301)。
        -   源RDS引擎：源RDS实例的引擎类型，不可变更。
        -   源RDS版本：源RDS实例的版本，不可变更。
        -   源RDS实例：可选的源RDS实例，不包括只读实例。
    -   从RDS迁移：先从RDS克隆数据，然后保持增量同步，主要用于迁移。在正式迁移切换前POLARDB为只读，且默认开启Binlog。详情请参见[一键升级RDS for MySQL到POLARDB for MySQL](../../../../intl.zh-CN/数据迁移__同步/POLARDB for MySQL/数据迁移/一键升级RDS for MySQL到POLARDB for MySQL.md#)。
        -   源RDS引擎：源RDS实例的引擎类型，不可变更。
        -   源RDS版本：源RDS实例的版本，不可变更。
        -   源RDS实例：可选的源RDS实例，不包括只读实例。
 |
    |可用区|集群的主可用区。     -   可用区是地域中的一个独立物理区域，不同可用区之间没有实质性区别。
    -   您可以选择将POLARDB与ECS创建在同一可用区或不同的可用区。
    -   您只需要选择主可用区，系统会自动选择备可用区。
 |
    |网络类型|     -   无需选择。
    -   仅支持专有网络VPC（Virtual Private Cloud）。VPC是一种隔离的网络环境，安全性和性能均高于传统的经典网络。
 |
    |VPC网络 VPC交换机

 |请确保POLARDB与需要连接的ECS创建于同一个VPC，否则它们无法通过内网互通，无法发挥最佳性能。     -   如果您已创建符合您网络规划的VPC，直接选择该VPC。例如，如果您已创建ECS，且该ECS所在的VPC符合您的规划，那么选择该VPC。
    -   如果您未创建符合您网络规划的VPC，您可以使用默认VPC和交换机：
        -   默认VPC：
            -   在您选择的地域中是唯一的。
            -   网段掩码是16位，如172.31.0.0/16，最多可提供65536个私网IP地址。
            -   不占用阿里云为您分配的VPC配额。
        -   默认交换机：
            -   在您选择的可用区中是唯一的。
            -   网段掩码是20位，如172.16.0.0/20，最多可提供4096个私网IP地址。
            -   不占用VPC中可创建交换机的配额。
    -   如果以上默认VPC和交换机无法满足您的要求，您可以自行创建VPC和交换机。
 |
    |配置|数据库引擎|     -   兼容MySQL 8.0（完全兼容）。原生支持并行查询，特定场景下（TPC-H测试）性能提升十倍。
    -   兼容MySQL 5.6（完全兼容）。
    -   兼容Oracle（高度兼容）。
 |
    |节点规格|按需选择。所有POLARDB节点均为独享型，性能稳定可靠。关于各规格的具体信息，请参见[规格与定价](../../../../intl.zh-CN/产品定价/规格与定价.md#)。|
    |节点个数|     -   无需选择。系统将自动创建一个与主节点规格相同的只读节点。
    -   如果主节点故障，系统会自动将只读节点切换为新的主节点，并重新生成一个只读节点。
    -   关于只读节点的更多信息，请参见[产品架构](../../../../intl.zh-CN/产品简介/产品架构.md#)。
 |
    |存储费用|无需选择。系统会根据实际数据使用量按小时计费，详情请参见[产品价格](../../../../intl.zh-CN/产品定价/规格与定价.md#)。 **说明：** 创建集群时无需选择存储容量，存储容量随数据量的增减而自动弹性伸缩。

 |

5.  设置**购买时长**（仅针对预付费集群）和**集群数量**，然后单击右侧的**立即购买**。 

    **说明：** 最多可以一次性创建50个集群，适用于游戏批量开服等业务场景。

6.  在确认订单页面，确认订单信息，阅读和勾选**服务协议**，单击**去支付**。

完成支付后，集群将在十分钟左右创建成功，您可在集群列表中看到创建的集群。

**说明：** 

-   当集群中的节点状态为**运行中**时，整个集群可能仍未创建完成，此时集群不可用。只有当集群状态为**运行中**时，集群才可以正常使用。
-   请确认已选中正确的地域，否则无法看到您创建的集群。

## 下一步 {#section_wtp_mam_dzq .section}

[设置集群白名单](../../../../intl.zh-CN/POLARDB for MySQL用户指南/设置集群白名单.md#)

## 相关API {#section_uxx_4pr_b3b .section}

|API|描述|
|:--|:-|
|[CreateDBCluster](../../../../intl.zh-CN/API参考/集群管理/CreateDBCluster.md#)|创建数据库集群|
|[DescribeDBClusters](../../../../intl.zh-CN/API参考/集群管理/DescribeDBClusters.md#)|查看集群列表|
|[DescribeDBClusterAttribute](../../../../intl.zh-CN/API参考/集群管理/DescribeDBClusterAttribute.md#)|查看指定POLARDB集群的详细属性|
|[DescribeAutoRenewAttribute](../../../../intl.zh-CN/API参考/集群管理/DescribeAutoRenewAttribute.md#)|查询POLARDB包年包月集群自动续费状态|
|[ModifyAutoRenewAttribute](../../../../intl.zh-CN/API参考/集群管理/ModifyAutoRenewAttribute.md#)|设置POLARDB包年包月集群自动续费状态|

