# Create a POLARDB cluster {#task_nhk_4qg_tdb .task}

This topic describes how to create a POLARDB cluster in the console. A POLARDB cluster contains one primary instance and a maximum of 15 read-only instances. \(At least one read-only instance is required to provide active-active high availability support\). An instance is a virtual database server, where you can create and manage multiple databases.

**Note:** 

-   POLARDB supports Virtual Private Cloud \(VPC\) networks only. VPC is an isolated network in Alibaba Cloud that is more secure than a classic network.

-   We recommend that you use POLARDB with Elastic Compute Service \(ECS\) and place them in the same VPC to achieve optimal performance. If your ECS instance is created in a classic network, you need to migrate it to VPC. For more information about how to migrate your instance to a VPC network, see [Migrate to VPC](https://help.aliyun.com/document_detail/55051.html).

****Prerequisites****

You must have registered an Alibaba Cloud account or created a Resource Access Management \(RAM\) user.

-   Click [here](https://account.alibabacloud.com/login/login.htm) to register an Alibaba Cloud account.

-   For more information about how to create and grant permissions to a RAM user, see [Create and authorize a RAM user](../../../../intl.en-US/User Guide for MySQL/Account Management/Create and authorize a RAM user.md#).


1.  Log on to your Alibaba Cloud account. 
    -   Click [here](https://account.alibabacloud.com/login/login.htm) to log on with your Alibaba Cloud account.

    -   Click [here](ttps://signin-intl.aliyun.com/login.htm) to log on with your RAM user. For more information, see [Log on as a RAM user](../../../../intl.en-US/User Guide for MySQL/Account Management/Create and authorize a RAM user.md#section_zb2_54q_tdb).

2.  Log on to the [POLARDB console](https://polardb.console.aliyun.com/).
3.  Click **Create Instance** in the upper-right corner.
4.  Select **Subscription** or **Pay-As-You-Go**. 
    -   **Subscription**: Pay for the DB servers of the primary instance and of a read-only instance by selecting either a monthly or annual subscription. Storage consumed by your POLARDB database is billed per GB/hour increments, and your payment is deducted from your account on an hourly basis. **Subscription** is more cost-effective for long term use. You can save more with longer subscription periods.
    -   **Pay-As-You-Go**: DB servers are billed per hour and storage consumed by your POLARDB database is billed per GB/hour based on actual increments. Your payment will be deducted from your account on an hourly basis. We recommend that you select **Pay-As-You-Go** for short term use.
5.  The POLARDB configuration parameters are described as follows. 

    |Console sections|Parameters|Descriptions|
    |:---------------|:---------|:-----------|
    |Basic Configurations|Regions|Select the region in which your cluster resides. You cannot change the region once you confirm your order.     -   We recommend that you select a region near the location of your target users to improve access speed. \[DO NOT TRANSLATE\]
    -   Make sure that you create your POLARDB cluster and the ECS to be connected in the same region. Otherwise, they cannot intercommunicate through an internal network and achieve optimal performance.
 |
    |Zone|     -   Zones are independent physical areas in one region. There are no differences between the zones.
    -   Your POLARDB cluster and the ECS instance that it needs to be connected can be located in the same zone or in different zones.
 |
    |Network Type|     -   There is no need to specify network type.
    -   POLARDB supports VPC networks only. VPC is an isolated virtual network and is more secure than a classic network.
 |
    |VPC Network VSwitch

 |Make sure that you place your POLARDB cluster and the ECS instance to be connected in the same VPC. Otherwise, they cannot intercommunicate through the intranet and achieve optimal performance.     -   Select the VPC if you have created a VPC that meets your network plan. For example, if you have created an ECS instance and the VPC it resides in meets your network plans, select this VPC.
    -   Alternatively, use the default VPC and VSwitch.
        -   Default VPC:
            -   It is a unique VPC in your selected region.
            -   The network mask for a default VPC has 16 bits, such as 172.31.0.0/16, providing up to 65,536 internal IP addresses.
            -   It is not counted against the total number of VPCs that you can create.
        -   Default VSwitch:
            -   It is a unique VSwitch in your selected region.
            -   The network mask for a default VSwitch has 20 bits, such as 172.16.0.0/20, providing up to 4,096 private IP addresses.
            -   It is not counted against the total number of Vswitches that you can create in a VPC.
    -   If the default VPC and VSwitch cannot satisfy your requirements, you can create your own VPC and VSwitch.
 |
    |Instance configuration|Database engine type|You do not need to specify.|
    |Instance specifications|Select a specification for your database instance according to your needs. All POLARDB instances own exclusive resources.|
    |Read-only instances|     -   You do not need to specify. By default, the system will create a read-only instance with the same specifications as the primary instance.
    -   If a primary instance fails, POLARDB will automatically promote the read-only instance as a primary instance, and generate a new read-only instance.
    -   For more information about read-only instances, see [Architecture](https://help.aliyun.com/document_detail/58766.html).
 |
    |Cluster name|     -   Optional
    -   The system will automatically create a name for your POLARDB cluster if you leave it blank. You can rename the cluster after it is created.
 |

    **Note:** You do not have to specify the storage size when you purchase a cluster. Based on your data volume usage, the storage capacity will automatically resize.

6.  Specify the **Duration** \(only applicable to Subscription instances\) and **Quantity**, and click **Buy Now**.
7.  On the Order Confirmation page, confirm your order information, read and accept the **Terms of Service**, and then click **Pay Now**. The POLARDB cluster will be created within 10 minutes after you complete the payment. You can view your clusters in the cluster list, and the primary instances and read-only instances of the clusters in the instance list.

    **Note:** 

    -   The cluster is unavailable and is still being created if some of the instances are in **Running**status. The cluster is only available when the status of the cluster is **Running**.

    -   Make sure that you have selected the correct region, or you cannot view your clusters or instances.


