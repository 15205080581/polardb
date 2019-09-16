# Upgrade RDS for MySQL to POLARDB for MySQL with one click {#concept_593020 .concept}

ApsaraDB for POLARDB allows you to upgrade an RDS for MySQL instance to a POLARDB for MySQL cluster with one click.

## ApsaraDB for POLARDB introduction {#section_hom_hgv_q2a .section}

ApsaraDB for POLARDB is the next-generation relational cloud database developed by Alibaba Cloud, which has the following main advantages.

-   Large storage capacity: up to 100 TB of storage.
-   High performance: up to 6x performance improvement over MySQL.
-   Serverless storage: no need to purchase storage capacity in advance, which is automatically scaled and is billed by usage.
-   Temporary upgrade: supports temporary upgrade of specifications to easily cope with short-term business peaks.

For more information, see [Benefits](../../../../intl.en-US/Product Introduction/Benefits.md#).

## Highlights {#section_4ty_tix_1xp .section}

-   Free-of-charge
-   Zero data loss during migration
-   Incremental data migration is supported. The service interruption period is less than 10 minutes.
-   Rollback is supported. The migration can be rolled back within 10 minutes after the migration fails.

## Migration process {#section_aoh_yoz_8jt .section}

1.  [Migrate data from the source RDS instance](#). This operation creates an ApsaraDB for POLARDB cluster with the same data as that of the source RDS instance. The incremental data of the source RDS instance will be synchronized to the ApsaraDB for POLARDB cluster in real time.

    **Note:** You need to change the database connection point in applications to that of the ApsaraDB for POLARDB cluster, verify that services are running properly, and click **Complete Migration** within 7 days. If you click **Complete Migration**, data synchronization stops between the source RDS instance and the destination ApsaraDB for POLARDB cluster.

2.  Click **Switch**. This operation sets the source RDS instance to the read-only mode and the destination ApsaraDB for POLARDB cluster to the read and write mode. The incremental data of the ApsaraDB for POLARDB cluster will be synchronized to the source RDS instance in real time. Modify the database connection point in applications.

    For more information about the procedure, see [Switch to the new cluster](#).

    **Note:** After you switch to the new cluster, you can also [roll back the migration](#).

3.  [Complete the migration](#).

## Precautions {#section_ldl_wsn_13b .section}

-   Data migration can only be performed in the same region.
-   The destination ApsaraDB for POLARDB cluster must contain information of the source RDS instance, including the account, database, IP address whitelist, and required parameters.
-   The parameters of the source RDS instance cannot be modified during migration.

## Prerequisites {#section_ezw_wsn_13b .section}

-   The source RDS instance is of the RDS for MySQL 5.6 high-availability version.
-   [Transparent Data Encryption \(TDE\)](../../../../intl.en-US/User Guide/Security/Set TDE.md#) and [Secure Sockets Layer \(SSL\)](../../../../intl.en-US/User Guide/Security/Configure SSL encryption.md#)are not enabled in the source RDS instance.
-   The table storage engine of the source RDS instance is InnoDB.

## Migrate data from the source RDS instance {#section_s4t_zsn_13b .section}

This operation creates an ApsaraDB for POLARDB cluster with the same data as that of the source RDS instance. The incremental data of the source RDS instance will be synchronized to the ApsaraDB for POLARDB cluster in real time.

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com).
2.  Click **Create Cluster**.
3.  Select Subscription or Pay-As-You-Go \(Hourly Rate\).
4.  Set parameters listed in the following table.

    |Parameter|Description|
    |---------|-----------|
    |**Region**|The region where the source RDS for MySQL instance resides. **Note:** The new ApsaraDB for POLARDB cluster is also located in this region.

 |
    |**Create Type**|The method of creating the cluster. Select **Migrate from RDS**.     -   **Default Create Type**: creates a new ApsaraDB for POLARDB cluster.
    -   **Clone from RDS**: clones the data of the selected RDS instance to an ApsaraDB POLARDB cluster.
    -   **Migration from RDS**: clones the data of the selected RDS instance to an ApsaraDB for POLARDB cluster and keeps the data synchronized between the RDS instance and the ApsaraDB for POLARDB cluster. The binlogging feature is enabled for the new cluster by default.
 |
    |**RDS Engine Type**|The engine type of the source RDS instance, which cannot be changed.|
    |**RDS Engine Version**|The engine version of the source RDS instance, which cannot be changed.|
    |**Source RDS instance**|The source RDS instances for selection, which do not include read-only instances.|
    |**Primary availability zone**| The zone of the instance. A zone is an independent physical area located within a region. There are no substantive differences between the zones.

 You can deploy the ApsaraDB for POLARDB cluster and the ECS instance in the same zone or in different zones.

 |
    |**Network Type**|The network type of the ApsaraDB for POLARDB cluster, which cannot be changed.|
    |**VPC** **Vswitch**

 |The VPC and VSwitch to which the ApsaraDB for POLARDB cluster belongs. Make sure that you place your ApsaraDB for POLARDB cluster and the ECS instance to be connected in the same VPC. Otherwise, they cannot communicate with each other through the internal network to achieve optimal performance.|
    |**Database Engine**|The database engine of the ApsaraDB for POLARDB cluster, which cannot be changed.|
    |**Node Specification**|The node specifications of the ApsaraDB for POLARDB cluster. Select the specifications as required. We recommend that you select specifications that are at least the same as those of the source RDS instance. All ApsaraDB for POLARDB nodes are dedicated ones with stable and reliable performance. For more information, see [Specifications and pricing](../../../../intl.en-US/Pricing/Specifications and pricing.md#).|
    |**Number Nodes**|The number of nodes. You do not need to specify this parameter. The system will create a read-only node with the same specifications as those of the primary node by default.|
    |**Storage Cost**|The storage capacity. You do not need to specify this parameter. The actual usage is billed hourly in pay-as-you-go mode. For more information, see [Specifications and pricing](../../../../intl.en-US/Pricing/Specifications and pricing.md#).|
    |**Cluster Name**|The cluster name for business distinguishing. The system will automatically create a name for your ApsaraDB for POLARDB cluster if you leave it blank. You can also modify the name after the cluster is created.|

5.  Specify **Duration** \(only applicable to subscription clusters\), and click **Buy Now** on the right side of the page.
6.  Confirm the order information, read the **Service Agreement**, select the checkbox to agree to it, and click **Activate Now**.
7.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com) and view the status of the new ApsaraDB for POLARDB cluster.

    **Note:** 

    -   After the cluster is created, it synchronizes data from the source RDS instance. You need to modify the database connection point in applications and click [Complete Migration](#) within 7 days. Otherwise, the data migration is canceled automatically.
    -   You can also cancel the migration in this step. For more information about the impact, see [FAQ](#).

## Switch to the new cluster {#section_jdh_0d3_zjz .section}

**Prerequisites**

-   [Data is migrated from the source RDS instance to the destination ApsaraDB for POLARDB cluster](#section_s4t_zsn_13b).
-   The value of **Replication Delay** is less than 60 seconds.

**Procedure**

After the prerequisites are met, you can switch to the destination ApsaraDB for POLARDB cluster, and change the database connection point in applications.

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com).
2.  Find the destination cluster and click the cluster ID.
3.  On the Basics page, click **Switch**. In the dialog box that appears, click **OK**.

    This operation sets the source RDS instance to the read-only mode and the destination ApsaraDB for POLARDB cluster to the read and write mode. The incremental data of the ApsaraDB for POLARDB cluster will be synchronized to the source RDS instance in real time.

    **Note:** 

    -   You cannot switch to the new cluster if the replication delay exceeds 60 seconds.
    -   The switch process generally takes less than 5 minutes.
4.  Refresh the page. When **POLARDB Read/Write Status** is **Read and Write**, change the database connection point in applications as soon as possible.

    **Note:** After you switch to the new cluster, you can also [roll back the migration](#).


## Complete the migration {#section_3ds_ojf_lmm .section}

[Migrate data from the source RDS instance](#section_s4t_zsn_13b)After data is migrated from the source RDS instance to the destination ApsaraDB for POLARDB cluster, you need to change the database connection point in applications and click **Complete Migration** within 7 days. This operation stops data synchronization between the RDS instance and the ApsaraDB for POLARDB cluster.

**Warning:** This operation stops data synchronization between the RDS instance and the ApsaraDB for POLARDB cluster, and the [rollback](#) feature is no longer available. We recommend that you use the ApsaraDB for POLARDB cluster for a period of time to verify that it runs properly before clicking Complete Migration.

1.  Log on to the [ApsaraDB for POLARDB console.](https://polardb.console.aliyun.com)
2.  Find the destination cluster and click the cluster ID.
3.  On the Basics page, click **Complete Migration**. In the dialog box that appears, click **OK**.

    **Note:** 

    -   After you click **OK**, the system stops data synchronization within 2 minutes. During this period, the **Complete Migration** button will not disappear. Do not click it repeatedly.
    -   You can choose whether to disable the binlogging feature for the ApsaraDB for POLARDB cluster. If this feature is disabled, the write performance can be improved slightly. However, you need to restart the ApsaraDB for POLARDB cluster.
4.  Release the source RDS instance if it is not needed.

## Roll back the migration {#section_hw4_hy4_13b .section}

After switching to the new cluster, you can also roll back the migration. By rolling back the migration, you restore the source RDS instance to the read and write mode and the destination ApsaraDB for POLARDB cluster to the read-only mode. Data of the source RDS instance will be synchronized to the destination ApsaraDB for POLARDB cluster. The procedure is as follows:

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com).
2.  Find the destination cluster and click the cluster ID.
3.  On the Basics page, click **Rollback**. In the dialog box that appears, click **OK.** 

    **Note:** After you click **OK**, the source RDS instance enters the read and write mode and the destination ApsaraDB for POLARDB cluster enters the read-only mode. Data of the source RDS instance will be synchronized to the destination ApsaraDB for POLARDB cluster. When **Source RDS Read/Write Status** is **Read and Write**, change the database connection point in applications to that of the RDS instance as soon as possible.


## FAQ {#section_lxr_3fp_13b .section}

-   Q: Will the source RDS instance be affected when **data is migrated** from the RDS instance?

    A: No, the source RDS instance can run properly.

-   Q: Will smooth migration affect business?

    A: Smooth migration ensures zero data loss during migration. The service interruption period is less than 10 minutes. You can roll back the migration if needed.

-   Q: What happens if I cancel the migration?

    A: If the migration is canceled, you can modify the parameters of the source RDS instance. The ApsaraDB for POLARDB cluster returns to the read and write mode, but will not be released. When canceling the migration manually, you can choose whether to disable the binlogging feature for the ApsaraDB for POLARDB cluster. The binlogging feature is not disabled if the migration is automatically canceled.


