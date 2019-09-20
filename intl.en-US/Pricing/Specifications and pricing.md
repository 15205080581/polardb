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
|Data backup|Free for now.|

## Prices for storage {#section_1mh_47i_7kk .section}

The storage is serverless. You do not need to select the storage capacity when you create a cluster. As data increases, the storage capacity automatically extends. The storage is billed based on the data size. You can check your data size on the Overview of your cluster in the console.

-   Regions in Mainland China: USD 0.00077/GB/hour.
-   Regions outside Mainland China: USD 0.00085/GB/hour.

**Note:** 

-   The storage capacity supports pay-as-you-go but not subscription.
-   The [maximum storage capacity](intl.en-US/Pricing/Specifications and pricing.md#table_g1y_xjg_tdb) varies with node specifications. If you want to increase the storage capacity, [upgrade the configuration of your cluster](../intl.en-US/User Guide for MySQL/Cluster management/Change specifications.md).

## Prices for data backup {#section_ssd_knn_d0p .section}

Currently, the storage occupied by ApsaraDB for POLARDB backup files is free of charge.

## Prices for compute nodes {#section_f4v_rpg_tdb .section}

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

|Node specification|Mainland China|China \(Hong Kong\)|US \(Silicon Valley\)|Singapore|Indonesia \(Jakarta\)|
|:-----------------|--------------|-------------------|---------------------|---------|---------------------|
|polar.mysql.x2.medium| USD 44/month

 USD 0.091/hour

 | USD 76/month

 USD 0.117/hour

 | USD 62/month

 USD 0.130/hour

 | USD 76/month

 USD 0.16/hour

 | USD 74/month

 USD 0.15/hour

 |
|polar.mysql.x4.large| USD 155/month

 USD 0.323/hour

 | USD 295/month

 USD 0.532/hour

 | USD 240/month

 USD 0.500/hour

 | USD 295/month

 USD 0.61/hour

 | USD 271/month

 USD 0.57/hour

 |
|polar.mysql.x4.xlarge| USD 310/month

 USD 0.646/hour

 | USD 589/month

 USD 1.063/hour

 | USD 480/month

 USD 1.000/hour

 | USD 589/month

 USD 1.23/hour

 | USD 542/month

 USD 1.13/hour

 |
|polar.mysql.x8.xlarge| USD 496/month

 USD 1.033/hour

 | USD 743/month

 USD 1.342/hour

 | USD 620/month

 USD 1.290/hour

 | USD 743/month

 USD 1.55/hour

 | USD 689/month

 USD 1.44/hour

 |
|polar.mysql.x8.2xlarge| USD 991/month

 USD 2.064/hour

 | USD 1,486/month

 USD 2.684/hour

 | USD 1,239/month

 USD 2.580/hour

 | USD 1,486/month

 USD 3.10/hour

 | USD 1,378/month

 USD 2.87/hour

 |
|polar.mysql.x8.4xlarge| USD 1,982/month

 USD 4.128/hour

 | USD 2,972/month

 USD 5.367/hour

 | USD 2,477/month

 USD 5.160/hour

 | USD 2,972/month

 USD 6.19/hour

 | USD 2,756/month

 USD 5.74/hour

 |
|polar.mysql.x8.12xlarge| USD 5,449/month

 USD 11.351/hour

 | USD 8,173/month

 USD 14.756/hour

 | USD 6,811/month

 USD 14.190/hour

 | USD 8,173/month

 USD 17.03/hour

 | USD 7,577/month

 USD 15.78/hour

 |

**Note:** 

-   **Each price in the preceding tables is for a single node. An ApsaraDB for POLARDB cluster consists of a primary node and a read-only node by default.**
-   You can select node specifications for the primary node when you create a cluster. The read-only node has the same specifications as the primary node.
-   Each **maximum input/output operations per second \(IOPS\)** value is theoretical.
-   The maximum connections of a cluster depend on the specifications of the nodes in the cluster. Increasing the number of nodes does not increase the maximum connections of the cluster.
-   If you need higher computing capabilities and storage capacity \(such as **100 TB**\), [open a ticket](https://workorder-intl.console.aliyun.com/console.htm?spm=5176.2020520001.console-base-top.dwork-order-1.497b4bd3uHPH0W#/ticket/createIndex) to contact after-sales support engineers.

## FAQ {#section_mxm_x1v_vfb .section}

-   **Q**: What is the price for an additional read-only node?

    **A**: A read-only node has the same price as the primary node in the same cluster. For more information, see [node specifications and prices](#) in this topic.

-   **Q**: Does an added read-only node double the storage capacity of a cluster?

    **A**: No. POLARDB separates its computing and storage capabilities. A read-only node that you purchase is only a compute node. It does not increase the storage capacity of a cluster.

    The storage is serverless. You do not need to select the storage capacity when you create a cluster. As data increases, the storage capacity automatically extends. The storage is billed based on the data size. The [maximum storage capacity](intl.en-US/Pricing/Specifications and pricing.md#table_g1y_xjg_tdb) varies with node specifications. If you want to increase the storage capacity, [upgrade the configuration of your cluster](../intl.en-US/User Guide for MySQL/Cluster management/Change specifications.md).


