# Specifications and pricing {#concept_zbj_4pg_tdb .concept}

## Billing methods {#section_d4v_rpg_tdb .section}

You can select either of the following billing methods for ApsaraDB for POLARDB clusters.

-   **Subscription**: When you create an ApsaraDB for POLARDB cluster, you need to pay for a compute cluster, including a primary node and a read-only node. The storage is billed by hour based on the data size. The fee for storage is deducted from your account by hour.

-   **Pay-as-you-go**: The compute cluster and the storage \(based on the data size\) are billed by hour. Fees are deducted from your account by hour.


## Billing items {#section_xzw_tfj_kgb .section}

The following table lists the billing items of an ApsaraDB for POLARDB cluster.

|Billing item|Description|
|------------|-----------|
|Compute cluster \(a primary node and a read-only node\)|You can select either **subscription** or **pay-as-you-go**.|
|Storage| -   You can select **pay-as-you-go**.
-   Or you can select subscription to purchase **a storage package**. For more information, see [Use a storage package](../intl.en-US/User Guide for MySQL/Cluster and instance management/Use a storage package.md#).

 |
|SQL explorer|SQL explorer supports **pay-as-you-go** after it is enabled. For more information, see [SQL explorer](../intl.en-US/User Guide for MySQL/SQL explorer.md#).|
|Data backup|Free for now.|

## Prices {#section_f4v_rpg_tdb .section}

-   **Prices for compute nodes**

    You can choose from the following POLARDB node specifications. Nodes of any specifications in POLARDB use exclusive resources. The CPU, memory, storage, and input/output \(I/O\) resources assigned to a node are exclusive to this node and not shared with other nodes. This improves the stability and reliability of the node.

    |Node specification|CPU and memory|Maximum storage capacity|Maximum connections|Internal network bandwidth|Maximum IOPS|I/O bandwidth|
    |:-----------------|:-------------|:-----------------------|:------------------|--------------------------|------------|-------------|
    |polar.mysql.x2.medium| Dual-core

 4 GB

 |5 TB|1,200|1 Gbit/s|8,000|1 Gbit/s|
    |polar.mysql.x4.large| Quad-core

 16 GB

 |10 TB|5,000|10 Gbit/s|32,000|4 Gbit/s|
    |polar.mysql.x4.xlarge| 8-core

 32 GB

 |10 TB|10,000|10 Gbit/s|64,000|8 Gbit/s|
    |polar.mysql.x8.xlarge| 8-core

 64 GB

 |30 TB|10,000|10 Gbit/s|72,000|10 Gbit/s|
    |polar.mysql.x8.2xlarge| 16-core

 128 GB

 |50 TB|20,000|10 Gbit/s|128,000|16 Gbit/s|
    |polar.mysql.x8.4xlarge| 32-core

 256 GB

 |50 TB|64,000|10 Gbit/s|192,000|24 Gbit/s|
    |polar.mysql.x8.12xlarge| 88-core

 710 GB

 |50 TB|64,000|25 Gbit/s|256,000|32 Gbit/s|

    **Note:** An ApsaraDB for POLARDB cluster with a dual-core CPU and 4 GB memory provides the basic specifications required in tests, trials, and low-load scenarios. We recommend that you do not use the basic specifications in a high-load production environment. In a high-load production environment, we recommend that you use an ApsaraDB for POLARDB cluster with an 8-core CPU and 32 GB memory or higher specifications.

    |Node specification|Mainland China|Hong Kong \(China\)|Singapore|
    |:-----------------|--------------|-------------------|---------|
    |polar.mysql.x2.medium| RMB 280/month

 RMB 0.59/hour

 | RMB 490/month

 RMB 0.75/hour

 | RMB 490/month

 RMB 1.02/hour

 |
    |polar.mysql.x4.large| RMB 1,000/month

 RMB 2.09/hour

 | RMB 1,900/month

 RMB 3.44/hour

 | RMB 1,900/month

 RMB 3.96/hour

 |
    |polar.mysql.x4.xlarge| RMB 2,000/month

 RMB 4.17/hour

 | RMB 3,800/month

 RMB 6.87/hour

 | RMB 3,800/month

 RMB 7.92/hour

 |
    |polar.mysql.x8.xlarge| RMB 3,200/month

 RMB 6.67/hour

 | RMB 4,800/month

 RMB 8.67/hour

 | RMB 4,800/month

 RMB 10.00/hour

 |
    |polar.mysql.x8.2xlarge| RMB 6,400/month

 RMB 13.34/hour

 | RMB 9,600/month

 RMB 17.34/hour

 | RMB 9,600/month

 RMB 20.00/hour

 |
    |polar.mysql.x8.4xlarge| RMB 12,800/month

 RMB 26.67/hour

 | RMB 19,200/month

 RMB 34.67/hour

 | RMB 19,200/month

 RMB 40.00/hour

 |
    |polar.mysql.x8.12xlarge| RMB 35,200/month

 RMB 73.34/hour

 | RMB 52,800/month

 RMB 95.34/hour

 | RMB 52,800/month

 RMB 110.00/hour

 |

    |Node specification|CPU and memory|Maximum storage capacity|Maximum connections|Internal network bandwidth|Maximum IOPS|I/O bandwidth|Price|
    |:-----------------|:-------------|:-----------------------|:------------------|--------------------------|------------|-------------|-----|
    |polar.pg.x4.medium| Dual-core

 8 GB

 |5 TB|400|1 Gbit/s|16,000|1 Gbit/s|See the prices in the console.|
    |polar.pg.x4.large| Quad-core

 16 GB

 |10 TB|800|10 Gbit/s|64,000|4 Gbit/s|
    |polar.pg.x4.xlarge| 8-core

 32 GB

 |10 TB|1,600|10 Gbit/s|128,000|8 Gbit/s|
    |polar.pg.x8.xlarge| 8-core

 64 GB

 |30 TB|3,200|10 Gbit/s|160,000|10 Gbit/s|
    |polar.pg.x8.2xlarge| 16-core

 128 GB

 |50 TB|6,400|10 Gbit/s|256,000|16 Gbit/s|
    |polar.pg.x8.4xlarge| 32-core

 256 GB

 |50 TB|12,800|10 Gbit/s|384,000|24 Gbit/s|
    |polar.pg.x8.12xlarge| 88-core

 710 GB

 |100 TB|36,000|25 Gbit/s|512,000|32 Gbit/s|

    |Node specification|CPU and memory|Maximum storage capacity|Maximum connections|Internal network bandwidth|Maximum IOPS|I/O bandwidth|Price|
    |:-----------------|:-------------|:-----------------------|:------------------|--------------------------|------------|-------------|-----|
    |polar.o.x4.medium| Dual-core

 8 GB

 |5 TB|400|1 Gbit/s|16,000|1 Gbit/s|See the prices in the console.|
    |polar.o.x4.large| Quad-core

 16 GB

 |10 TB|800|10 Gbit/s|64,000|4 Gbit/s|
    |polar.o.x4.xlarge| 8-core

 32 GB

 |10 TB|1,600|10 Gbit/s|128,000|8 Gbit/s|
    |polar.o.x8.xlarge| 8-core

 64 GB

 |30 TB|3,200|10 Gbit/s|160,000|10 Gbit/s|
    |polar.o.x8.2xlarge| 16-core

 128 GB

 |50 TB|6,400|10 Gbit/s|256,000|16 Gbit/s|
    |polar.o.x8.4xlarge| 32-core

 256 GB

 |50 TB|12,800|10 Gbit/s|384,000|24 Gbit/s|
    |polar.o.x8.12xlarge| 88-core

 710 GB

 |100 TB|36,000|25 Gbit/s|512,000|32 Gbit/s|

    **Note:** 

    -   ****Each price in the preceding tables is for a single node. An ApsaraDB for POLARDB cluster consists of a primary node and a read-only node by default.****
    -   You can select node specifications for the primary node when you create a cluster. The read-only node has the same specifications as the primary node.
    -   Each **maximum input/output operations per second \(IOPS\)** value is theoretical.
    -   The maximum connections of a cluster depend on the specifications of the nodes in the cluster. Increasing the number of nodes does not increase the maximum connections of the cluster.
    -   If you need higher computing capabilities and storage capacity \(such as **100 TB**\), [open a ticket](https://selfservice.console.aliyun.com/ticket/createIndex) to contact after-sales support engineers.
-   **Prices for storage**

    The storage is serverless. You do not need to select the storage capacity when you create a cluster. As data increases, the storage capacity automatically extends. The storage is billed based on the data size. You can check your data size on the [details page](../intl.en-US/User Guide for MySQL/Cluster and instance management/View cluster and instance details.md#) of your cluster in the console.

    -   Regions in Mainland China: RMB 0.00486/GB/hour
    -   Hong Kong \(China\): RMB 0.00542/GB/hour
    -   Other regions outside Mainland China: RMB 0.00542/GB/hour
    **Note:** 

    -   The storage capacity supports pay-as-you-go but not subscription.
    -   The [maximum storage capacity](intl.en-US/Pricing/Specifications and pricing.md#table_g1y_xjg_tdb) varies with node specifications. If you want to increase the storage capacity, [upgrade the configuration of your cluster](../intl.en-US/User Guide for MySQL/Cluster and instance management/Change specifications.md).
    We recommend that you purchase a storage package if your data size is large. The storage package can be shared by all the clusters in a specified region. For more information, see [Use a storage package](../intl.en-US/User Guide for MySQL/Cluster and instance management/Use a storage package.md#).

-   **Prices for SQL explorer**

    SQL explorer is billed based on the storage capacity of audit logs.

    -   Regions in Mainland China: RMB 0.008/GB/hour
    -   Regions outside Mainland China: RMB 0.0122/GB/hour
    **Note:** The storage capacity of audit logs supports pay-as-you-go but not subscription.

-   **Prices for data backup**

    Currently, the storage occupied by ApsaraDB for POLARDB backup files is free of charge.


## FAQ {#section_mxm_x1v_vfb .section}

-   **Q**: What is the price for an additional read-only node?

    **A**: A read-only node has the same price as the primary node in the same cluster. For more information, see [node specifications and prices](#) in this topic.

-   **Q**: Does an added read-only node double the storage capacity of a cluster?

    **A**: No. POLARDB separates its computing and storage capabilities. A read-only node that you purchase is only a compute node. It does not increase the storage capacity of a cluster.

    The storage is serverless. You do not need to select the storage capacity when you create a cluster. As data increases, the storage capacity automatically extends. The storage is billed based on the data size. The [maximum storage capacity](intl.en-US/Pricing/Specifications and pricing.md#table_g1y_xjg_tdb) varies with node specifications. If you want to increase the storage capacity, [upgrade the configuration of your cluster](../intl.en-US/User Guide for MySQL/Cluster and instance management/Change specifications.md).


