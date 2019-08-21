# Migrate data from Amazon Aurora MySQL to POLARDB for MySQL {#concept_jl1_mw3_kgb .concept}

## Background {#section_mhf_p1t_lgb .section}

This topic describes how to migrate data from Amazon Aurora MySQL to Alibaba Cloud POLARDB for MySQL by using Alibaba Cloud [Data Transmission Service \(DTS\)](https://www.alibabacloud.com/help/product/26590.htm).

## Prerequisites {#section_zj4_fxs_lgb .section}

-   The source instance can be connected through the public network.
-   An Amazon Aurora instance that supports MySQL 5.6 is created.
-   [An ApsaraDB for POLARDB cluster is created](../../../../intl.en-US/Quick Start for MySQL/Create a POLARDB cluster.md#).
-   [An account with the read and write permissions is created](../../../../intl.en-US/Quick Start for MySQL/Create an initial account for a POLARDB cluster.md#).

## Limits {#section_z23_3xs_lgb .section}

-   You can migrate data only from Amazon Aurora MySQL 5.6.
-   Schema migration for events is not available.
-   DTS reads floating-point values \(including float values and double values\) in a column of the MySQL database by using the round \(column,precision\) method. If the value precision is not specified, the precision is 38 for float values and 308 for double values. Therefore, you must check whether the migration precision meets your service expectations.
-   If object name mapping is enabled for an object, other objects depending on this object may fail to be migrated.
-   If incremental data migration is selected, binlogging must be enabled for the source MySQL instance.
-   If incremental data migration is selected, the binlog\_format parameter of the source database must be set to row.
-   If incremental data migration is selected and the source MySQL version is 5.6, the binlog\_row\_image parameter must be set to full.
-   If binlog file ID disorder occurs in the source MySQL instance because of cross-host migration or reconstruction during incremental data migration, the incremental data being migrated may be lost.

## Precautions {#section_ewl_lxs_lgb .section}

-   We recommend that you back up data before performing migration tasks.

-   DTS attempts to recover abnormal tasks executed within seven days. This may lead to data in the source database overwriting the service data that has been written to the destination database. Therefore, after a migration task is completed, you must run the `revoke` command to revoke the **write permission** of the DTS account that is used to access the destination instance.


## Procedure {#section_uwt_sck_5fb .section}

1.  Log on to the Amazon Aurora instance. Click the name of the source database and view the endpoint and port of the database in the connection information.
2.  Log on to the [DTS console](https://dts.console.aliyun.com/).
3.  In the left-side navigation pane, click **Data Migration**. In the right pane, click **Create Migration Task** in the upper-right corner.
4.  \(Optional\) Set the task name.

    DTS generates a name for each task automatically. The task name is not required to be unique. You can change the task name as needed. We recommend that you choose an informative name so that the task can be easily identified.

5.  Configure information about the source and destination databases. The following table describes the parameters.

    |Database type|Parameter|Description|
    |-------------|---------|-----------|
    |Source Database|Instance Type|The type of the source instance. Select User-Created Database with Public IP Address.|
    |Instance Region|The region where the source database resides. If you have configured access control for your instance, you need to allow the public IP address range of the specified region to access the instance before configuring a migration task. **Note:** You can click **Get IP Address Segment of DTS** to view and copy the IP address range of the region.

 |
    |Database Type|The source database type. Select MySQL.|
    |Hostname or IP Address|The endpoint of the Amazon Aurora database.|
    |Port Number|The port of the Amazon Aurora database.|
    |Database Account|The account with the read and write permissions on the Amazon Aurora database.|
    |Database Password|The password of the Amazon Aurora database account.|
    |Destination Database|Instance Type|The type of the destination instance. Select POLARDB.|
    |Instance Region|The region where the destination instance resides.|
    |POLARDB Instance ID|The ID of the destination instance in the selected region.|
    |Database Account|The account with the read and write permissions on the destination instance.|
    |Database Password|The password of the account for accessing the destination instance.|

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/95598/156636763337255_en-US.png)

6.  Click **Test Connectivity** and verify that the test results for both the source and target databases are Passed.
7.  Click **Set Whitelist and Next** in the lower-right corner of the page.
8.  Select the migration type. In the Available section, select the objects to be migrated, and click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/95598/156636763337264_en-US.png) to move the objects to the Selected section.

    **Note:** To maintain data consistency before and after migration, we recommend that you select Schema Migration, Full Data Migration, and Incremental Data Migration.

    Currently, Schema Migration and Full Data Migration are free of charge, while Incremental Data Migration charges the users by hour based on link specifications.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/95598/156636763437261_en-US.png)

9.  Click **Precheck** and wait until the precheck ends.

    **Note:** If the precheck fails, you can fix the problems as instructed and run the precheck again.

10. Click **Next**. In the **Confirm Settings** dialog box that appears, read the **Data Transmission Service \(Pay-As-You-Go\) Service Terms**, select the checkbox to agree to them, and then click **Buy and Start**.

    If you select Incremental Data Migration, DTS synchronizes the data changes in the source database to the destination ApsaraDB for POLARDB cluster during incremental data migration. The migration task does not stop automatically. If you only want to migrate data, we recommend that you stop data writing to the source database for a few minutes when there is no delay in incremental data migration. After the incremental data migration enters the no-delay status again, stop the migration task and switch the services to the destination ApsaraDB for POLARDB cluster.

11. Select the destination region to view the migration status. The status will be **Completed** when the migration is completed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/95598/156636763637263_en-US.png)

    Data is migrated from Amazon Aurora MySQL to POLARDB for MySQL.


