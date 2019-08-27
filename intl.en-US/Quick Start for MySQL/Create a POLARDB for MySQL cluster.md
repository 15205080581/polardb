# Create a POLARDB for MySQL cluster {#task_1580301 .task}

This topic describes how to create a POLARDB for MySQL cluster in the POLARDB console.

You have registered an Alibaba Cloud account or created a Resource Access Management \(RAM\) user.

-   Click [here](https://account.alibabacloud.com/login/login.htm) to register an Alibaba Cloud account.
-   For more information about how to create and grant permissions to a RAM user, see [Create and authorize a RAM user](../../../../intl.en-US/User Guide for MySQL/Account Management/Create and authorize a RAM user.md#).

A POLARDB for MySQL cluster contains one primary node and up to 15 read-only nodes. \(At least one read-only node is required to provide active-active high availability support\). A node is a virtual DB server, where you can create and manage one or more databases.

**Note:** 

-   POLARDB supports Virtual Private Clouds \(VPCs\) only. A VPC is an isolated network in Alibaba Cloud that is more secure than a classic network.
-   We recommend that you use POLARDB with Elastic Compute Service \(ECS\) and place them in the same VPC to achieve optimal performance. If your ECS instance is created in a classic network, you must migrate it to a VPC.

## Procedure {#section_drs_p4r_b3b .section}

1.  Log on to Alibaba Cloud. 
    -   Click [here](https://account.alibabacloud.com/login/login.htm) to log on with your Alibaba Cloud account.
    -   Click [here](ttps://signin-intl.aliyun.com/login.htm) to log on with your RAM user. For more information, see [Log on as a RAM user](../../../../intl.en-US/User Guide for MySQL/Account Management/Create and authorize a RAM user.md#section_zb2_54q_tdb).
2.  Log on to the [POLARDB console](https://polardb.console.aliyun.com/).
3.  Click **Create Cluster**.
4.  Select **Subscription** or **Pay-As-You-Go**. 
    -   **Subscription**: Pay for the DB servers of the primary node and of a read-only node by selecting either a monthly or annual subscription. Storage consumed by your POLARDB database is billed per GB/hour increments, and your payment is deducted from your account on an hourly basis. The **Subscription** billing method is more cost-effective for long term use. You can save more with longer subscription periods.
    -   **Pay-As-You-Go**: DB servers are billed per hour and storage consumed by your POLARDB database is billed per GB/hour based on actual increments. Your payment is deducted from your account on an hourly basis. We recommend that you select the **Pay-As-You-Go** billing method for short term use.
5.  Set the following parameters. 

    |Console section|Parameter|Description|
    |:--------------|:--------|:----------|
    |**Basic**|Region|Select the region in which your cluster resides. You cannot change the region once you confirm your order. **Note:** The POLARDB cluster must be located in the same region as the ECS instance to be connected. Otherwise, you can connect the POLARDB cluster to the ECS instance only through the Internet, which may degrade performance.

 |
    |Primary Availability Zone|The primary zone of the POLARDB cluster.     -   Zones are independent physical areas in a region. The zones in the same region are basically the same.
    -   The POLARDB cluster and the ECS instance to be connected can be located in the same zone or in different zones.
    -   You only need to select a primary zone. The system automatically assigns a secondary zone.
 |
    |Network Type|     -   You do not need to specify the network type.
    -   POLARDB supports VPCs only. A VPC is an isolated virtual network and is more secure than a classic network.
 |
    |VPC Network VSwitch

 |Make sure that you place your POLARDB cluster and the ECS instance to be connected in the same VPC. Otherwise, they cannot intercommunicate through the intranet and achieve optimal performance.     -   Select the VPC if you have created a VPC that meets your network plan. For example, if you have created an ECS instance and the VPC where it resides meets your network plan, select this VPC.
    -   Alternatively, use the default VPC and VSwitch.
        -   Default VPC:
            -   It is a unique VPC in your selected region.
            -   The network mask for a default VPC has 16 bits, such as 172.31.0.0/16, providing up to 65,536 private IP addresses.
            -   It is not counted against the total number of VPCs that you can create.
        -   Default VSwitch:
            -   It is a unique VSwitch in your selected region.
            -   The network mask for a default VSwitch has 20 bits, such as 172.16.0.0/20, providing up to 4,096 private IP addresses.
            -   It is not counted against the total number of Vswitches that you can create in a VPC.
    -   If the default VPC and VSwitch cannot satisfy your requirements, you can create your own VPC and VSwitch.
 |
    |**Instance**|Database Engine|     -   Fully compatible with MySQL 8.0
    -   Fully compatible with MySQL 5.6
    -   Fully compatible with PostgreSQL 11
    -   Highly compatible with Oracle
 |
    |Node Specification|Select a specification for your database node according to your needs. All POLARDB nodes own exclusive resources.|
    |Number Nodes|     -   You do not need to specify the number. By default, the system creates one read-only node with the same specifications as the primary node.
    -   If a primary node fails, the system automatically promotes the read-only node as a primary node and generates a new read-only node.
    -   For more information about read-only nodes, see [Architecture](https://www.alibabacloud.com/help/doc-detail/58766.htm).
 |
    |Storage Cost|You do not need to specify the storage cost. The system calculates the fees by hour based on the storage usage. For more information, see [Specifications and pricing](../../../../intl.en-US/Pricing/Specifications and pricing.md#). **Note:** You do not need to specify the storage capacity of the POLARDB cluster. The storage capacity automatically scales based on the data volume.

 |

6.  Specify the **Purchase Plan** \(only applicable to Subscription clusters\) and **Number**, and click **Buy Now**. 

    **Note:** You can create up to 50 POLARDB clusters at a time when, for example, you want to roll out games in batches.

7.  On the Order Confirmation page, confirm your order information, select **ApsaraDB for POLARDB Pay-As-You-Go Agreement of Service**, and then click **Pay Now**. The POLARDB cluster will be created within 10 minutes after you complete the payment. You can view the POLARDB cluster in the cluster list, and the primary and read-only nodes of the POLARDB cluster in the node list.

    **Note:** 

    -   If some of the nodes are in the **Running**state, the POLARDB cluster is unavailable and is still being created. The POLARDB cluster is only available when the cluster status is **Running**.
    -   Make sure that you have selected the correct region, or you cannot view the POLARDB cluster or the nodes in it.

## APIs {#section_uxx_4pr_b3b .section}

|API|Description|
|:--|:----------|
|[CreateDBCluster](../../../../intl.en-US/API Reference/Cluster management/CreateDBCluster.md#)|Used to create a POLARDB cluster.|
|[DescribeDBClusters](../../../../intl.en-US/API Reference/Cluster management/DescribeDBClusters.md#)|Used to list POLARDB clusters.|
|[DescribeDBClusterAttribute](../../../../intl.en-US/API Reference/Cluster management/DescribeDBClusterAttribute.md#)|Used to view the attributes of a POLARDB cluster.|
|[DescribeAutoRenewAttribute](../../../../intl.en-US/API Reference/Cluster management/DescribeAutoRenewAttribute.md#)|Used to query the automatic renewal status of a POLARDB cluster that uses the Subscription billing method.|
|[ModifyAutoRenewAttribute](../../../../intl.en-US/API Reference/Cluster management/ModifyAutoRenewAttribute.md#)|Used to set the automatic renewal status of a POLARDB cluster that uses the Subscription billing method.|

