# Migrate data from RDS for MySQL to POLARDB for MySQL {#concept_pf2_25y_bgb .concept}

**Note:** Alibaba Cloud has supported the feature for upgrading Relational Database Service \(RDS\) for MySQL to POLARDB for MySQL with one click. For more information, see [Upgrade RDS for MySQL to POLARDB for MySQL with one click](intl.en-US/Data migration__synchronization/POLARDB for MySQL/Data migration/Upgrade RDS for MySQL to POLARDB for MySQL with one click.md#).

You can migrate data from RDS for MySQL to POLARDB for MySQL by using Alibaba Cloud [Data Transmission Service \(DTS\)](https://www.alibabacloud.com/help/doc-detail/26592.htm). By using the storage engine of DTS incremental data migration, you can migrate data to the destination POLARDB for MySQL cluster without interrupting the source RDS instance.

This topic describes how to migrate data from RDS for MySQL to POLARDB for MySQL by using DTS.

## Migration permission requirements {#section_lrw_l1y_bgb .section}

When DTS is used to migrate data from the source RDS instance and the destination ApsaraDB for POLARDB cluster, the account of the source RDS instance must have the read and write permissions, and the account of the destination ApsaraDB for POLARDB cluster must have all permissions on the migration object.

## Procedure {#section_owb_pby_bgb .section}

This section describes how to use DTS to migrate data from the RDS for MySQL instance to the ApsaraDB for POLARDB cluster.

**Create migration accounts** 

When you configure a migration task, you need to provide the account of the source RDS instance and the account of the destination ApsaraDB for POLARDB cluster. For more information about permissions required for the migration accounts, see Migration permission requirements. If you have not created the migration accounts, create [an account for RDS for MySQL](https://www.alibabacloud.com/help/doc-detail/26186.htm) and [an account for POLARDB for MySQL](../../../../intl.en-US/Quick Start for MySQL/Create an initial account for a POLARDB cluster.md#). First, create a migration account for the source and destination instances respectively. Then, grant the created accounts the permissions to read data from and write data to the tables or databases to be migrated.

**Configure a migration task** 

After all the preceding prerequisites are met, you can start to configure a migration task. This section describes the procedure for configuring a migration task.

1.  Log on to the [DTS console](https://dts.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**.
3.  In the upper-right corner, click **Create Migration Task**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79403/156636690636105_en-US.png)

4.  \(Optional\) Set the task name.

    DTS generates a name for each task automatically. The task name is not required to be unique. You can change the task name as needed. We recommend that you choose an informative name so that the task can be easily identified.

5.  Enter the information of the source instance.

    -   Instance Type: Select **RDS Instance**.
    -   Instance Region: Select the region where the source RDS instance resides.
    -   RDS Instance ID: Select the ID of the source RDS instance to be migrated.
    -   Database Account: Enter the account for accessing the RDS instance.
    -   Database Password: Enter the password of the account.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79403/156636690934082_en-US.png)

6.  Click **Test Connectivity** and verify that DTS can connect to the source RDS instance.
7.  Enter the information of the destination ApsaraDB for POLARDB cluster.

    -   Instance Type: Select **POLARDB**.
    -   Instance Region: Select the region where the ApsaraDB for POLARDB cluster resides.
    -   POLARDB Instance ID: Select the ID of the destination ApsaraDB for POLARDB cluster to which data is migrated.
    -   Database Account: Enter the account for accessing the ApsaraDB for POLARDB cluster.
    -   Database Password: Enter the password of the account.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79403/156636691034083_en-US.png)

8.  Click **Test Connectivity** and verify that DTS can connect to the destination ApsaraDB for POLARDB cluster.
9.  Click **Set Whitelist and Next** in the lower-right corner of the page. In this step, DTS adds the IP address of the DTS server to the whitelists of the source RDS instance and the destination ApsaraDB for POLARDB cluster. This prevents connection issues where the DTS service cannot connect to the required source RDS instance and destination ApsaraDB for POLARDB cluster for data migration.
10. Set **Migration Type** and **Migration Object**.

    -   **Migration Type**:

        -   Schema Migration

            DTS migrates the schema definitions of the migration objects to the destination cluster. Currently, DTS supports schema migration only for tables. For other objects such as views, synonyms, triggers, stored procedures, stored functions, packages, and user-defined data types, schema migration is not supported.

        -   Full Data Migration

            DTS migrates all data of the migration objects to the destination cluster.

        -   Incremental data migration

            DTS synchronizes the data changes in the source instance during the migration to the destination cluster. If a Data Definition Language \(DDL\) operation is performed during the migration, the schema changes will not be synchronized to the destination cluster.

        If you only need to migrate full data, select Schema Migration and Full Data Migration as the migration types.

        If you need to migrate data without service interruption, select Schema Migration, Full Data Migration, and Incremental Data Migration as the migration types.

        **Note:** Both Schema Migration and Full Data Migration are free of charge, while Incremental Data Migration charges the users.

    -   **Migration Object**: Select the objects to be migrated in the Available section, and then click the right arrow to add them to the Selected section.

        The migration objects can be databases, tables, and columns. By default, after an object is migrated to the destination cluster, the object name remains the same as that of the object in the source instance. If the object you migrate has different names in the source instance and destination cluster, you need to use the object name mapping feature provided by DTS. For more information, see [Mappings of database, table, and column](https://www.alibabacloud.com/help/doc-detail/26628.htm).

        **Note:** 

        -   Currently, system tables cannot be migrated.
        -   Ensure that the name of an object is unique after it is migrated to the destination instance. To change the name of an object before it is migrated the destination instance, move the pointer over the object in the Selected section, and then click **Edit**.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79403/156636691234085_en-US.png)

11. Click **Precheck** in the lower-right corner. After the precheck ends, click **Next**.

    If the precheck fails, you can click the Info icon in the Result column of each failed item to view the details. Fix the problems as instructed and run the precheck again.

12. Confirm your DTS order information. Read the **Terms of Service**, select the checkbox to agree to it, and click **Buy and Start**.

    After the precheck succeeds, you can start the migration task and check the migration status and progress in the task list.

    If you select Incremental Data Migration, DTS synchronizes the data changes in the source database to the destination ApsaraDB for POLARDB cluster during incremental data migration. The migration task does not stop automatically. If you only want to migrate data, we recommend that you stop data writing to the source database for a few minutes when there is no delay in incremental data migration. After the incremental data migration enters the no-delay status again, stop the migration task and switch the services to the destination ApsaraDB for POLARDB cluster.

13. Select the destination region to view the migration status. The status will be **Completed** when the migration is completed.

    Data is migrated from RDS for MySQL to POLARDB for MySQL.


