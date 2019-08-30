# Migrate data from local MySQL to POLARDB for MySQL {#concept_rmt_hrm_4gb .concept}

You can migrate data from a local MySQL instance to a POLARDB for MySQL cluster by using Alibaba Cloud [Data Transmission Service \(DTS\)](https://www.alibabacloud.com/help/doc-detail/26592.htm). By using the storage engine of DTS incremental data migration, you can migrate data from the local MySQL instance to the POLARDB for MySQL cluster without interrupting the services of local applications.

This topic describes how to migrate data from local MySQL to POLARDB for MySQL by using DTS.

## SQL operations supported for incremental data migration {#section_zrx_vb4_4gb .section}

For incremental data migration from **local MySQL** to **POLARDB for MySQL**, DTS supports the following SQL operations:

INSERT, UPDATE, DELETE, and REPLACE

ALTER TABLE, ALTER VIEW, ALTER FUNCTION, and ALTER PROCEDURE

CREATE DATABASE, CREATE SCHEMA, CREATE INDEX, CREATE TABLE, CREATE PROCEDURE, CREATE

FUNCTION, CREATE TRIGGER, CREATE VIEW, and CREATE EVENT

DROP FUNCTION, DROP EVENT, DROP INDEX, DROP PROCEDURE, DROP TABLE, DROP TRIGGER, and DROP

VIEW

RENAME TABLE and TRUNCATE TABLE

## Prerequisites {#section_f4w_2f4_4gb .section}

-   You have [created a POLARDB for MySQL cluster](../../../../intl.en-US/Quick Start for MySQL/Create a POLARDB for MySQL cluster.md#).
-   You have [created an account with the read and write permissions on the POLARDB for MySQL cluster](../../../../intl.en-US/Quick Start for MySQL/Create accounts for a POLARDB for MySQL cluster.md#).
-   You have granted the account the remote access permission on the local MySQL instance. The authorization command is grant all privileges on \*.\* to <username\>@'<ipaddress\>' identified by "<password\>";.

    **Note:** 

    -   <username\>: the username for accessing the local MySQL database.
    -   <ipaddress\>: the IP address for logging on to the database. The value localhost indicates that you can only log on to the database locally. The value % indicates that you can use any IP address to log on to the database.
    -   <password\>: the password of the username for accessing the local MySQL database.

## Precautions {#section_xbb_nd4_4gb .section}

-   We recommend that you back up data before performing migration tasks.
-   DTS attempts to recover abnormal tasks executed within seven days. This may lead to data in the source database overwriting the service data that has been written to the destination database. Therefore, after a migration task is completed, you must run the `revoke` command to revoke the **write permission** of the DTS account that is used to access the destination instance.

## Restrictions {#section_wrp_xtm_4gb .section}

-   Only MySQL 5.6 is supported for the migration.
-   Schema migration for events is not available.
-   DTS reads floating-point values \(including float values and double values\) in a column of the MySQL database by using the round \(column,precision\) method. If the value precision is not specified, the precision is 38 for float values and 308 for double values. Therefore, you must check whether the migration precision meets your service expectations.
-   If object name mapping is enabled for an object, other objects depending on this object may fail to be migrated.
-   If incremental data migration is selected, binlogging must be enabled for the source MySQL instance.
-   If incremental data migration is selected, the binlog\_format parameter of the source database must be set to row.
-   If incremental data migration is selected and the source MySQL version is 5.6, the binlog\_row\_image parameter must be set to full.
-   If binlog file ID disorder occurs in the source MySQL instance because of cross-host migration or reconstruction during incremental data migration, the incremental data being migrated may be lost.

## Migration permission requirements {#section_gmj_3tm_4gb .section}

When DTS is used to migrate data from **local MySQL** to **POLARDB for MySQL**, the required permissions of the migration accounts on the source instance and destination cluster vary depending on the migration types. The following table lists the migration types and required permissions.

|Database type|Schema migration|Full data migration|Incremental data migration|
|-------------|----------------|-------------------|--------------------------|
|Local MySQL instance|select|select| super

 select

 replication slave

 replication client

 |
|POLARDB for MySQL cluster|Read and write permissions|Read and write permissions|Read and write permissions|

## Migration process {#section_stx_xg4_4gb .section}

To solve the dependency conflicts between objects and improve the migration success rate when migrating data from **local MySQL** to **POLARDB for MySQL**, DTS defines the following migration steps for schema objects and data:

1.  Migrate the following schema objects: tables and views.
2.  Migrate data in full mode.
3.  Migrates the following schema objects: stored procedures, functions, triggers, and foreign keys.
4.  Migrate data in incremental mode.

**Note:** If incremental data migration is not selected, after full data migration is completed, the migration progress in the task list is 100% for schema migration and 100% for full data migration. The migration status is **Migrating**. At this time, the migration task is migrating the objects defined in the third step. Do not end the task in this status. Otherwise, the migrated data may be inconsistent.

## Procedure {#section_uwt_sck_5fb .section}

1.  Log on to the [DTS console](https://dts-intl.console.aliyun.com).
2.  Click **Data Migration** in the left-side navigation pane, and then click **Create Migration Task** in the upper-right corner.
3.  \(Optional\) Set the task name.

    DTS generates a name for each task automatically. The task name is not required to be unique. You can change the task name as needed. We recommend that you choose an informative name so that the task can be easily identified.

4.  Configure information about the source and destination databases. The following table describes the parameters.

    |Database type|Parameter|Description|
    |-------------|---------|-----------|
    |Source database|Instance Type|The type of the source database instance. Select User-Created Database with Public IP Address.|
    |Instance Region|The region where the local MySQL instance resides.|
    |Database Type|The type of the source database. Select MySQL.|
    |Hostname or IP Address|The public IP address of the source database.|
    |Port Number|The listening port of the source database.|
    |Database Account|The account with the read and write permissions on the source database.|
    |Database Password|The password of the account for accessing the source database.|
    |Destination database|Instance Type|The type of the destination instance. Select POLARDB.|
    |Instance Region|The region where the POLARDB for MySQL cluster resides.|
    |POLARDB Instance ID|The ID of the destination instance in the selected region.|
    |Database Account|The account with the read and write permissions on the destination instance.|
    |Database Password|The password of the account for accessing the destination instance.|

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120364/156715619738182_en-US.png)

5.  Click **Test Connectivity**. Ensure that both the source and destination databases pass the test.
6.  Click **Set Whitelist and Next**.
7.  Select the migration types and migration objects.******** 

    -   **Migration types**:

        -   Schema migration

            DTS migrates the schema definitions of the migration objects to the destination cluster. DTS currently supports the following objects for schema migration: tables, views, triggers, stored procedures, and stored functions.

        -   Full data migration

            DTS migrates all data of the migration objects to the destination cluster. Concurrent inserts are performed during full data migration, resulting in segments in the tables of the destination instance. After a full data migration task is completed, the tablespace of the destination instance is larger than that of the source instance.

            If you only select full data migration, the data written to the local MySQL instance during the migration is not synchronized to the destination POLARDB for MySQL cluster.

        -   Incremental data migration

            DTS synchronizes the data changes in the source instance during the migration to the destination cluster. If a Data Definition Language \(DDL\) operation is performed during the migration, the schema changes will not be synchronized to the destination cluster.

        If you only need to perform full data migration, select schema migration and full data migration as the migration types.

        If you need to migrate data without service interruption, select schema migration, full data migration, and incremental data migration as the migration types.

        **Note:** Both schema migration and full data migration are free of charge, while incremental data migration charges the users.

    -   **Migration objects**: Select the objects to be migrated in the Available section, and then click the right arrow to add them to the Selected section.

        The migration objects can be databases, tables, and columns. By default, after an object is migrated to the destination cluster, the object name remains the same as that of the object in the source instance. If the object you migrate has different names in the source instance and destination cluster, you need to use the object name mapping feature provided by DTS. For more information, see [Mappings of database, table, and column names](https://www.alibabacloud.com/help/doc-detail/26628.htm).

        **Note:** 

        -   Currently, system tables cannot be migrated.
        -   Ensure that the name of an object is unique after it is migrated to the destination instance. To change the name of an object before it is migrated the destination instance, move the pointer over the object in the Selected section, and then click **Edit**.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120364/156715619738183_en-US.png)

8.  Click **Precheck**. After the precheck is successful, click **Next**.

    **Note:** If the precheck fails, you can click the Info icon in the Result column of each failed item to view the details. Fix the problems as instructed and run the precheck again.

9.  Confirm your DTS order information, read the **Data Transmission Service \(Pay-As-You-Go\) Service Terms**, select the check box to agree to them, and then click **Buy and Start**.

    If you select incremental data migration, DTS synchronizes the data changes in the source instance during the migration to the destination cluster. The migration task does not stop automatically. If you only want to migrate data, we recommend that you stop data writing to the source database for a few minutes when there is no delay in incremental data migration. After the incremental data migration enters the no-delay status again, stop the migration task and switch the services to the POLARDB for MySQL cluster.

10. Select the destination region to view the migration status. The status changes to **Finished** when the migration is completed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/120364/156715619738209_en-US.png)

    Then, you have completed data migration from local MySQL to POLARDB for MySQL.


