# Specifications and pricing

This topic describes the specifications and pricing of Apsara PolarDB, including billing methods, billing items, and compute nodes, the pricing of storage capacity, data backups, SQL Explorer, and GDN.

## Billing methods

Apsara PolarDB clusters support the following billing methods:

-   Subscription

    If you choose the subscription billing method, you must pay in advance for the compute cluster \(for example, a primary node and a read-only node\) that you create. Storage resources are still billed based on the per-hour usage. The charge is deducted from your account balance on an hourly basis.

-   Pay-as-you-go \(pay by hour\)

    If you choose the pay-as-you-go billing method, you pay for the resources after you use them. Regardless of the compute clusters or storage space, you are billed by hour. The charge is deducted from your account balance on an hourly basis.


## Billing items

The following table lists the billing items of an Apsara PolarDB cluster.

|Billing items|Billing method|
|-------------|--------------|
|[Compute node pricing](#section_1wh_nb8_bqu)|**Subscription** or **pay as you go \(pay by hour\)**.|
|[SQL Explorer pricing](#section_b4f_b7j_vmy)|After you enable SQL Explorer, the billing method is specified as **Pay-as-you-go**. For more information, see [SQL Explorer](/intl.en-US/User Guide/Diagnostics and optimization/SQL Explorer.md).|
|[Storage space](#section_u9d_n9d_3jt)|**Pay by hour**.|
|[Data backup](#section_ryg_gsw_hmu)|This feature is available for free. You are only charged for the storage space of backup files. For more information, see [Back up data](/intl.en-US/User Guide/Backup and restore/Back up data.md).|
|[Global Database Network \(GDN\)](#section_y7y_dnz_rx2)|GDN is free of charge. You are only charged for the compute nodes that use GDN. For more information, see [GDN](/intl.en-US/User Guide/Deployment Architecture/Global database networks/Create a GDN and a secondary cluster.md).|

## Compute node pricing

All nodes in Apsara PolarDB clusters are hosted on dedicated resources. The CPU, memory, storage, and resources allocated to a node are exclusive to this node. This improves the stability and reliability of the node. The following table lists all types of nodes that are available.

|Node type|CPU and memory|Storage capacity|Maximum number of connections|Internal network bandwidth|Maximum number of IOPS|I/O bandwidth|
|:--------|:-------------|:---------------|:----------------------------|--------------------------|----------------------|-------------|
|polar.mysql.x4.medium|2 cores

8GB

|5TB|1,200|1Gbps|8000|1Gbps|
|polar.mysql.x4.large|4 cores

16GB

|10TB|5,000|10Gbps|32,000|4Gbps|
|polar.mysql.x4.xlarge|8 cores

32GB

|10TB|10,000|10Gbps|64,000|8Gbps|
|polar.mysql.x8.xlarge|8 cores

64GB

|30TB|10,000|10Gbps|72,000|10Gbps|
|polar.mysql.x8.2xlarge|16 cores

128GB

|50TB|20,000|10Gbps|128,000|16Gbps|
|polar.mysql.x8.4xlarge|32 cores

256GB

|50TB|64,000|10Gbps|192,000|24Gbps|
|polar.mysql.x8.12xlarge|88 cores

710GB

|100TB|64,000|25Gbps|256,000|32Gbps|

**Note:** An Apsara PolarDB cluster with a 2-core CPU and 8-GB memory provides the basic specifications required in tests, trials, and other scenarios with light load. We recommend that you do not use this type of clusters in a load-heavy production environment. We recommend that you use an Apsara PolarDB cluster with an 8-core CPU and 32-GB memory or higher specifications.

|Parameter|Mainland China|China \(Hong Kong\)|US \(Silicon Valley\)|Singapore \(Singapore\)|Indonesia \(Jakarta\)|Malaysia \(Kuala Lumpur\)|Germany \(Frankfurt\)|India \(Mumbai\)|US \(Virginia\)|Japan \(Tokyo\)|
|Node type|CPU and memory|
|:--------|--------------|-------------------|---------------------|-----------------------|---------------------|-------------------------|---------------------|----------------|---------------|---------------|
|:--------|--------------|
|polar.mysql.x4.medium|2 cores

 8 GB

|USD 44/month

 USD 0.091/hour

|USD 76/month

 USD 0.117/hour

|USD 62/month

 USD 0.128 /hour

|USD 76/month

 USD 0.159 /hour

|USD 74/month

 USD 0.15/hour

|USD 76/month

 USD 0.159 /hour

|USD 67/month

 USD 0.139 /hour

|USD 61 /month

 USD 0.126 /hour

|USD 50 /month

 USD 0.104 /hour

|USD 64 /month

 USD 0.133 /hour |
|polar.mysql.x4.large|Quad-core

 16 GB

|USD 155/month

 USD 0.323/hour

|USD 295/month

 USD 0.532/hour

|USD 240/month

 USD 0.501 /hour

|USD 295/month

 USD 0.613 /hour

|USD 271/month

 USD 0.57/hour

|USD 295/month

 USD 0.613 /hour

|USD 264/month

 USD 0.549 /hour

|USD 233 /month

 USD 0.484 /hour

|USD 202 /month

 USD 0.42 /hour

|USD 248 /month

 USD 0.516 /hour |
|polar.mysql.x4.xlarge|8 cores

 32 GB

|USD 310/month

 USD 0.646/hour

|USD 589/month

 USD 1.063/hour

|USD 480/month

 USD 1.001 /hour

|USD 589/month

 USD 1.226 /hour

|USD 542/month

 USD 1.13/hour

|USD 589/month

 USD 1.226 /hour

|USD 527/month

 USD 1.097 /hour

|USD 480/month

 USD 1 /hour

|USD 403 /month

 USD 0.839 /hour

|USD 496/month

 USD 1.032 /hour |
|polar.mysql.x8.xlarge|8 cores

 64 GB

|USD 496/month

 USD 1.033/hour

|USD 743/month

 USD 1.342/hour

|USD 620/month

 USD 1.291 /hour

|USD 743/month

 USD 1.548 /hour

|USD 689/month

 USD 1.44/hour

|USD 743/month

 USD 1.548 /hour

|USD 651/month

 USD 1.355 /hour

|USD 604 /month

 USD 1.258 /hour

|USD 496/month

 USD 1.032 /hour

|USD 635 /month

 USD 1.323 /hour |
|polar.mysql.x8.2xlarge|16 cores

 128 GB

|USD 991/month

 USD 2.064/hour

|USD 1,486/month

 USD 2.684/hour

|USD 1,239/month

 USD 2.58 /hour

|USD 1,486/month

 USD 3.096 /hour

|USD 1,378/month

 USD 2.87/hour

|USD 1,486/month

 USD 3.096 /hour

|USD 1,301/month

 USD 2.709 /hour

|USD 1208 /month

 USD 2.516 /hour

|USD 991/month

 USD 2.064/hour

|USD 1270 /month

 USD 2.645 /hour |
|polar.mysql.x8.4xlarge|32 cores

 256 GB

|USD 1,982/month

 USD 4.128/hour

|USD 2,972/month

 USD 5.367/hour

|USD 2,477/month

 USD 5.16 /hour

|USD 2,972/month

 USD 6.192 /hour

|USD 2,756/month

 USD 5.74/hour

|USD 2,972/month

 USD 6.192 /hour

|USD 2,601/month

 USD 5.418 /hour

|USD 2415 /month

 USD 5.031 /hour

|USD 1,982/month

 USD 4.128/hour

|USD 2539 /month

 USD 5.289 /hour |
|polar.mysql.x8.12xlarge|88-core

 710 GB

|USD 5,449/month

 USD 11.351/hour

|USD 8,173/month

 USD 14.756/hour

|USD 6,811/month

 USD 14.189 /hour

|USD 8,173/month

 USD 17.026 /hour

|USD 7,577/month

 USD 15.78/hour

|USD 8,173/month

 USD 17.026 /hour

|USD 7,229/month

 USD 15.059 /hour

|USD 6640 /month

 USD 10.061 /hour

|USD 5,449/month

 USD 11.351/hour

|USD 6981 /month

 USD 14.543 /hour |

**Note:**

-   **The preceding table lists the prices of a single node. An Apsara PolarDB cluster consists of a primary node and a read-only node by default.**
-   You can select a node type for the primary node when you create a cluster. The same type will be automatically applied to read-only nodes.
-   The **maximum number of IOPS** is a theoretically calculated value.
-   The maximum number of connections for a cluster depends on the specifications of nodes, and does not change with the number of nodes.
-   If you require higher computing performance and larger storage space \(for example, **100 TB**\), you can [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm?spm=5176.2020520001.console-base-top.dwork-order-1.497b4bd3uHPH0W#/ticket/createIndex) to contact after-sales services.

## Storage pricing

The storage refers to the space for cluster data files, system files, log files \(online logs and archived logs\), and temporary files.

**Note:** After you purchase an Apsara PolarDB cluster, the system automatically creates the preceding files required for regular database operations. The files occupy certain storage space.

**Pay-as-you-go**

Storage resources are provisioned in a serverless architecture. Therefore, you do not need to specify the storage space when you purchase an Apsara PolarDB cluster. The cluster automatically expands the storage as the data size increases. You are only billed for the storage space that you have used. You can view the storage space that you have used on the Basic Information page in the console.

-   The price for regions in mainland China: USD 0.00077/GB/hour.
-   The price for China \(Hong Kong\) and other regions outside mainland China: USD 0.00085/GB/hour.

**Note:** The storage capacity varies with the node specifications. If 90% of the storage space is used, the system sends SMS messages and emails to you on a daily basis. If you want to expand the storage capacity, upgrade your clusters. For more information, see [Change specifications](/intl.en-US/User Guide/Elastic upgrade and downgrade/Change specifications.md#) .

If you need to store large amounts of data, for example, 1,000 GB data or more, storage packages are more cost-effective than the pay-as-you-go billing method. Larger discounts are provided for the storage packages that contain higher storage capacities.

## Data backup pricing

The backup and restoration features of Apsara PolarBD are free of charge. Only storage fees are charged. Fees are calculated based on the storage consumed by backups \(cluster and log data\) and the retention period of these backups. For more information about how to use backup feature, see [Back up data](/intl.en-US/User Guide/Backup and restore/Back up data.md).

|Region|Level-1 backup|Level-2 backup|Log backup|
|------|--------------|--------------|----------|
|Mainland China|USD 0.000464/GB/hour|USD 0.0000325/GB/hour|USD 0.0000325/GB/hour|
|Hong Kong \(China\) and regions outside China|USD 0.000650/GB/hour|USD 0.0000455/GB/hour|USD 0.0000455/GB/hour|

|Backup type|Free quota|Billing method|
|-----------|----------|--------------|
|Level-1 backups|Database storage usage × 50% You can view the storage space that you have used on the **Basic Information** page in the console.

|Storage fee per hour = \(The total physical storage of level-1 backups - Free quota\) × Unit price per hour -   You can use level-1 backups for free within the free quota.
-   Figure 1 shows the **total physical storage of the level-1 backups**.

![The total physical storage of level-1 backups](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7038449951/p103440.png)


For example, if the total physical storage of the level-1 backups is 700 GB and database storage usage is 1,000 GB, then the storage fee per hour is USD 0.0928.

The fee is calculated based on the following formula: \[700 GB - \(1,000 GB × 50%\)\] × USD 0.000464 = USD 0.0928. |
|Level-2 backups|None|Storage fee per hour = The total physical storage of level-2 backups × Unit price per hour For example, if the total physical storage of level-2 backups is 1,000 GB, the storage fee per hour is USD 0.0325.

The fee is calculated based on the following formula: 1,000 GB × USD 0.0000325 = USD 0.0325. |
|Log backup|100GB|Storage fee per hour = \(The total physical storage of log backups - 100GB\) × Unit price per hour For example, if the total physical storage of log backups is 1,000 GB. The storage fee per hour is USD 0.02925.

The fee is calculated based on the following formula: \(1,000 GB - 100 GB\) × USD 0.0000325 = USD 0.02925. |

## SQL Explorer pricing

You are billed based on the storage space consumed by audit logs.

-   The price for regions in mainland China: USD 0.0013/GB/hour.
-   The price for China \(Hong Kong\) and other regions outside mainland China: USD 0.0019/GB/hour.

**Note:** Audit logs are billed only on a pay-as-you-go basis.

## Global Database Network \(GDN\)

GDN supports free cross-regional transmission and only charges you for Apsara PolarDB clusters. For more information about the billing items of Apsara PolarDB clusters, see [Compute node pricing](#section_1wh_nb8_bqu) .

## FAQ

-   Q: What is the price if I want to add a read-only node?

    A: For an Apsara PolarDB cluster, a read-only node is billed at the same price as the primary node. For more information, see [Compute node pricing](#section_1wh_nb8_bqu).

-   Q: Is the maximum storage capacity doubled after I add a read-only node?

    A: No, Apsara PolarDB clusters run in a compute-storage separated architecture. Read-only nodes are used for computing. Adding read-only nodes does not change the storage capacity of the cluster.

    Storage resources are provisioned in a serverless architecture. Therefore, you do not need to specify the storage space when you create a cluster. The cluster automatically expands the storage as the data size increases. You are only billed for the storage space that you have used. The storage capacity varies with node types. If you want to expand the storage capacity, [upgrade your clusters](/intl.en-US/User Guide/Elastic upgrade and downgrade/Change specifications.md).


