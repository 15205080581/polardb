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
|Storage| You can select **pay-as-you-go**.

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

    |Node specification|Jakarta|
    |:-----------------|-------|
    |polar.mysql.x2.medium| USD 74/month

 USD 0.15/hour

 |
    |polar.mysql.x4.large| USD 271/month

 USD 0.57/hour

 |
    |polar.mysql.x4.xlarge| USD 542/month

 USD 1.13/hour

 |
    |polar.mysql.x8.xlarge| USD 689/month

 USD 1.44/hour

 |
    |polar.mysql.x8.2xlarge| USD 1,378/month

 USD 2.87/hour

 |
    |polar.mysql.x8.4xlarge| USD 2,756/month

 USD 5.74/hour

 |
    |polar.mysql.x8.12xlarge| USD 7,577/month

 USD 15.78/hour

 |

    |Node specification|CPU and memory|Maximum storage capacity|Maximum connections|Internal network bandwidth|Maximum IOPS|I/O bandwidth|
    |:-----------------|:-------------|:-----------------------|:------------------|--------------------------|------------|-------------|
    |polar.pg.x4.medium| Dual-core

 8 GB

 |5 TB|400|1 Gbit/s|16,000|1 Gbit/s|
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

    |Node specification|Mainland China|Hong Kong \(China\)|US West|
    |------------------|--------------|-------------------|-------|
    |polar.pg.x4.medium| USD 795.6/year

 USD 78/month

 USD 0.163/hour

 | USD 1509.6/year

 USD 148/month

 USD 0.226/hour

 | USD 1224/year

 USD 120/month

 USD 0.202/hour

 |
    |polar.pg.x4.large| USD 1581/year

 USD 155/month

 USD 0.324/hour

 | USD 3009/year

 USD 295/month

 USD 0.533/hour

 | USD 2448/year

 USD 240/month

 USD 0.434/hour

 |
    |polar.pg.x4.xlarge| USD 3162/year

 USD 310/month

 USD 0.646/hour

 | USD 6007.8/year

 USD 589/month

 USD 1.064/hour

 | USD 4896/year

 USD 480/month

 USD 0.867/hour

 |
    |polar.pg.x8.xlarge| USD 5059.2/year

 USD 496/month

 USD 1.033/hour

 | USD 7578.6/year

 USD 743/month

 USD 1.342/hour

 | USD 6324/year

 USD 620/month

 USD 1.12/hour

 |
    |polar.pg.x8.2xlarge| USD 10108.2/year

 USD 991/month

 USD 2.065/hour

 | USD 15157.2/year

 USD 1486/month

 USD 2.684/hour

 | USD 12637.8/year

 USD 1239/month

 USD 2.237/hour

 |
    |polar.pg.x8.4xlarge| USD 20216.4/year

 USD 1982/month

 USD USD 4.128/hour

 | USD 30314.4/year

 USD 2972/month

 USD 5.367/hour

 | USD 25265.4/year

 USD 2477/month

 USD 4.472/hour

 |
    |polar.pg.x8.12xlarge| USD 55579.8/year

 USD 5449/month

 USD 11.352/hour

 | USD 83364.6/year

 USD 8173/month

 USD 14.757/hour

 | USD 69472.2/year

 USD 6811/month

 USD 12.297/hour

 |

    |Node specification|CPU and memory|Maximum storage capacity|Maximum connections|Internal network bandwidth|Maximum IOPS|I/O bandwidth|
    |:-----------------|:-------------|:-----------------------|:------------------|--------------------------|------------|-------------|
    |polar.o.x4.medium| Dual-core

 8 GB

 |5 TB|400|1 Gbit/s|16,000|1 Gbit/s|
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

    |Node specification|Mainland China|
|Monthly Subscription price|Yearly Subscription price|Hourly Pay-As-You-Go price|
    |------------------|--------------|
    |--------------------------|-------------------------|--------------------------|
    |polar.o.x4.medium|USD 161|USD 1642.2|USD 0.336|
    |polar.o.x4.large|USD 322|USD 3284.4|USD 0.672|
    |polar.o.x4.xlarge|USD 644|USD 6568.8|USD 1.342|
    |polar.o.x8.xlarge|USD 830|USD 8466|USD 1.729|
    |polar.o.x8.2xlarge|USD 1660|USD 16932|USD 3.458|
    |polar.o.x8.4xlarge|USD 3319|USD 33853.8|USD 6.914|
    |polar.o.x8.12xlarge|USD 9126|USD 93085.2|USD 19.013|

    **Note:** 

    -   **Each price in the preceding tables is for a single node. An ApsaraDB for POLARDB cluster consists of a primary node and a read-only node by default.**
    -   You can select node specifications for the primary node when you create a cluster. The read-only node has the same specifications as the primary node.
    -   Each **maximum input/output operations per second \(IOPS\)** value is theoretical.
    -   The maximum connections of a cluster depend on the specifications of the nodes in the cluster. Increasing the number of nodes does not increase the maximum connections of the cluster.
    -   If you need higher computing capabilities and storage capacity \(such as **100 TB**\), [open a ticket](https://selfservice.console.aliyun.com/ticket/createIndex) to contact after-sales support engineers.
-   **Prices for storage**

    The storage is serverless. You do not need to select the storage capacity when you create a cluster. As data increases, the storage capacity automatically extends. The storage is billed based on the data size. You can check your data size on the [details page](../intl.en-US/User Guide for MySQL/Cluster and instance management/View cluster and instance details.md#) of your cluster in the console.

    |Billing methods|Mainland China|Hong Kong \(China\)|US West|Jakarta|
    |---------------|--------------|-------------------|-------|-------|
    |Subscription（USD/GB/month）|0.55|0.61|0.59|0.66|
    |pay-as-you-go（USD/GB/hour）|0.00077|0.00085|0.00085|0.00085|

    **Note:** 

    -   The [maximum storage capacity](intl.en-US/Pricing/Specifications and pricing.md#table_g1y_xjg_tdb) varies with node specifications. If you want to increase the storage capacity, [upgrade the configuration of your cluster](../intl.en-US/User Guide for MySQL/Cluster and instance management/Change specifications.md).
-   **Prices for data backup**

    Currently, the storage occupied by ApsaraDB for POLARDB backup files is free of charge.


## FAQ {#section_mxm_x1v_vfb .section}

-   **Q**: What is the price for an additional read-only node?

    **A**: A read-only node has the same price as the primary node in the same cluster. For more information, see [node specifications and prices](#) in this topic.

-   **Q**: Does an added read-only node double the storage capacity of a cluster?

    **A**: No. POLARDB separates its computing and storage capabilities. A read-only node that you purchase is only a compute node. It does not increase the storage capacity of a cluster.

    The storage is serverless. You do not need to select the storage capacity when you create a cluster. As data increases, the storage capacity automatically extends. The storage is billed based on the data size. The [maximum storage capacity](intl.en-US/Pricing/Specifications and pricing.md#table_g1y_xjg_tdb) varies with node specifications. If you want to increase the storage capacity, [upgrade the configuration of your cluster](../intl.en-US/User Guide for MySQL/Cluster and instance management/Change specifications.md).


