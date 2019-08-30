# Migrate data from ECS-hosted MySQL to POLARDB for MySQL {#concept_ybs_vzx_bgb .concept}

You can migrate data from an Elastic Compute Service \(ECS\)-hosted MySQL instance to a POLARDB for MySQL cluster by using Alibaba Cloud [Data Transmission Service \(DTS\)](https://www.alibabacloud.com/help/doc-detail/26592.htm). Incremental data migration allows you to migrate data to the POLARDB for MySQL cluster without service interruption of the source instance.

## Migration permission requirements {#section_lrw_l1y_bgb .section}

When configuring a migration task, you need to provide the migration accounts for the ECS-hosted MySQL instance and the POLARDB for MySQL cluster. The following table lists the migration types and required permissions.

**Note:** If you have not created the migration accounts, create [an account for ECS-hosted MySQL](https://dev.mysql.com/doc/refman/8.0/en/grant.html) and [an account for POLARDB for MySQL](../intl.en-US/Quick Start for MySQL/Create accounts for a POLARDB for MySQL cluster.md#) and grant the accounts the required permissions.

|Database type|Schema migration|Full data migration|Incremental data migration|
|:------------|:---------------|:------------------|:-------------------------|
|ECS-hosted MySQL instance|SELECT permission on migration objects|SELECT permission on migration objects|SELECT, REPLICATION CLIENT, and REPLICATION SLAVE permissions on migration objects|
|POLARDB for MySQL cluster|ALL permissions on migration objects|ALL permissions on migration objects|ALL permissions on migration objects|

## Configure a migration task {#section_owb_pby_bgb .section}

1.  Log on to the [DTS console](https://www.alibabacloud.com/help/doc-detail/99729.htm).
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the upper-right corner of the Data Migration page, click **Create Migration Task**.
4.  Configure information about the source and destination databases.

    ![Configure information about the source and destination databases](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78734/156715649940718_en-US.png)

    |Item|Parameter|Description|
    |:---|:--------|:----------|
    |Task Name|-|     -   DTS generates a name for each task automatically. The task name is not required to be unique.
    -   You can change the task name as needed. We recommend that you choose an informative name so that the task can be easily identified.
 |
    |Source Database|Instance Type|The type of the source database instance. Select **User-Created Database in ECS Instance**.|
    |Instance Region|The region where the ECS instance resides.|
    |ECS Instance ID|The ID of the ECS Instance.|
    |Database Type|The type of the source database. Select **MySQL**.|
    |Port Number|The port for the ECS-hosted MySQL instance to provide services. Default value: 3306.|
    |Database Account|The account for accessing the source database.|
    |Database Password|The password of the account for accessing the source database.|
    |Encryption|The encryption mode for accessing the source database. Select **Non-encrypted** or **SSL-encrypted**. In this example, **Non-encrypted** is selected. **Note:** If SSL encryption is required, you need to prepare and upload your CA root certificate in advance.

 |
    |Destination Database|Instance Type|The type of the destination database instance. Select **POLARDB**.|
    |Instance Region|The region where the POLARDB for MySQL cluster resides.|
    |POLARDB Instance ID|The ID of the POLARDB for MySQL cluster.|
    |Database Account|The account for accessing the destination database.|
    |Database Password|The password of the account for accessing the destination database.|

5.  Click **Set Whitelist and Next**.

    **Note:** In this step, the IP address of the DTS server is automatically added to the whitelist of the POLARDB for MySQL cluster to ensure that the server can connect to the cluster. After the migration is completed, you can remove the IP address from the whitelist. For more information, see [Configure a whitelist for a POLARDB for MySQL cluster](../intl.en-US/Quick Start for MySQL/Configure a whitelist for a POLARDB for MySQL cluster.md#).

6.  Select the migration types and migration objects.

    |Parameter|Description|
    |:--------|:----------|
    |Migration Types|     -   If you only need to perform full data migration, select **Schema Migration** and **Full Data Migration** as the migration types.

**Note:** To ensure data consistency, do not write new data into the source database during full data migration.

    -   If you need to migrate data without service interruption, select **Schema Migration**, **Full Data Migration**, and **Incremental Data Migration**.
 |
    |Available|     -   Select the objects to be migrated in the **Available** section, and then click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78734/156715650040720_en-US.png) to add them to the **Selected** section.
    -   The migration objects can be databases, tables, and columns.
    -   By default, after an object is migrated to the destination cluster, the object name remains the same as that of the object in the source instance. If the object you migrate has different names in the source instance and destination cluster, you need to use the object name mapping feature provided by DTS. For more information, see [Mappings of database, table, and column names](https://www.alibabacloud.com/help/doc-detail/26628.htm).
 |

7.  Click **Precheck**.

    **Note:** 

    -   A precheck is performed before the migration task starts. The migration task can be started only after the precheck is successful.
    -   If the precheck fails, click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/86903/156715650035996_en-US.png) corresponding to each failed item to view the details. Fix the problems as instructed and run the precheck again.
8.  After the precheck is successful, click **Next**.
9.  On the **Confirm Settings** page, set **Channel Specification** read the **Data Transmission Service \(Pay-As-You-Go\) Service Terms**, and then select the check box to agree to them.
10. Click **Buy and Start** to start the migration task.
    -   Full data migration

        Wait until the migration task stops automatically.

    -   Incremental data migration

        The migration task does not stop automatically. We recommend that you stop data writing to the source database for a few minutes when there is no delay in incremental data migration. After the incremental data migration enters the no-delay status again, stop the migration task.

11. After the migration is completed, switch the services to the POLARDB for MySQL cluster at an appropriate time based on the business needs.

