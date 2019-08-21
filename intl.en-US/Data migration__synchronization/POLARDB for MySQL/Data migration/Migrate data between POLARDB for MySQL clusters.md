# Migrate data between POLARDB for MySQL clusters {#concept_d1p_4zn_v2b .concept}

This topic describes how to migrate data from one POLARDB for MySQL cluster to another by using [Data Transmission Service \(DTS\)](https://help.aliyun.com/document_detail/26592.html). This migration service is free of charge.

## Prerequisite {#section_e5z_1rk_xdb .section}

**Set an IP address whitelist for the source cluster**

Before data migration, you need to set a whitelist for the source POLARDB for MySQL cluster. To set a whitelist, follow these steps:

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select the region where the source POLARDB for MySQL cluster resides.
3.  Find the target cluster and click the cluster ID in the Cluster Name column.****
4.  In the Access Information section, click **Configure** next to a whitelist, and then add the Classless Inter-Domain Routing \(CIDR\) block of DTS in the dialog box that appears.

    |Region|CIDR block to be added to the whitelist|
    |------|---------------------------------------|
    |China \(Hangzhou\)|101.37.14.0/24,114.55.89.0/24,115.29.198.0/24,118.178.120.0/24,118.178.121.0/24,120.26.106.0/24,120.26.116.0/24,120.26.117.0/24,120.26.118.0/24,120.55.192.0/24,120.55.193.0/24,120.55.194.0/24,120.55.241.0/24,121.40.125.0/24,121.196.246.0/24,101.37.12.0/24,101.37.13.0/24,101.37.15.0/24,101.37.25.0/24,47.96.39.0/24,118.31.184.0/24,118.31.165.0/24,118.31.246.0/24,120.55.12.0/24,47.97.7.0/24,120.55.129.0/24|
    |China \(Shanghai\)|139.196.17.0/24,139.196.18.0/24,139.196.25.0/24,139.196.27.0/24,139.196.154.0/24,139.196.116.0/24,139.196.254.0/24,139.196.166.0/24,106.14.46.0/24,106.14.37.0/24,106.14.36.0/24,106.15.250.0/24,101.132.248.0/24,47.100.95.0/24,120.55.129.0/24|
    |China \(Beijing\)|112.126.80.0/24,112.126.87.0/24,112.126.91.0/24,112.126.92.0/24,123.56.108.0/24,123.56.120.0/24,123.56.137.0/24,123.56.148.0/24,123.56.164.0/24,123.57.48.0/24,182.92.153.0/24,182.92.186.0/24,101.200.174.0/24,101.200.160.0/24,101.200.176.0/24,47.94.36.0/24,47.94.47.0/24,101.201.214.0/24,101.201.82.0/24,120.55.129.0/24|


**Create migration accounts**

Before data migration, you need to create a migration account for the source and destination POLARDB for MySQL clusters respectively. You can create privileged accounts. For more information, see [Create a database account](../../../../intl.en-US/Quick Start for MySQL/Create an initial account for a POLARDB cluster.md#).

**Stop writing data to the source cluster**

To ensure data consistency during migration, stop writing data to the POLARDB for MySQL cluster before the migration starts.

## Procedure {#section_yww_nrk_xdb .section}

1.  Log on to the [DTS console](https://dts.console.aliyun.com/).
2.  Click **Data Migration** in the left-side navigation pane, and then click **Create Migration Task**.
3.  \(Optional\) Set the task name.

    DTS generates a name for each task automatically. The task name is not required to be unique. You can change the task name as needed. We recommend that you choose an informative name so that the task can be easily identified.

4.  Configure information about the source cluster.

    -   Instance Type: the type of the source database instance. Select **User-Created Database with Public IP Address**.
    -   Instance Region: the region where the source cluster resides.
    -   Database Type: the type of the source database. Select **MySQL**.
    -   Hostname or IP Address: the public connection point of the source cluster. For more information, see [View the connection point](intl.en-US/Quick Start for MySQL/View database connection strings.md).
    -   Port Number: the listening port of the source cluster. Set this parameter to 3306.
    -   Database Account: the account for accessing the source cluster.
    -   Database Password: the password of the account for accessing the source cluster.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17772/15663535839778_en-US.png)

5.  Click **Test Connectivity**. Ensure that the source cluster passes the test.
6.  Configure information about the destination cluster.
    -   Instance Type: the type of the destination database instance. Select **POLARDB**.
    -   Instance Region: the region where the destination cluster resides.
    -   POLARDB Instance ID: the ID of the destination cluster.
    -   Database Account: the account for accessing the destination cluster.
    -   Database Password: the password of the account for accessing the destination cluster.
7.  Click **Test Connectivity**. Ensure that the destination cluster passes the test.
8.  Click **Set Whitelist and Next**.
9.  Select the migration types and migration objects.******** 
    -   **Migration types**: Select **Schema Migration** and **Full Data Migration**. \(Currently, incremental data migration is not supported.\) To ensure data consistency during migration, stop writing data to the POLARDB for MySQL cluster before the migration starts.
        -   Schema migration

            DTS migrates the schema definitions of the migration objects to the destination cluster. Currently, DTS supports schema migration only for tables. For other objects such as views, synonyms, triggers, stored procedures, stored functions, packages, and user-defined data types, schema migration is not supported.

        -   Full data migration

            DTS migrates all data of the migration objects to the destination cluster.

    -   **Migration objects**: Select the objects to be migrated in the Available section, and then click the right arrow to add them to the Selected section.

        **Note:** 

        -   Currently, system tables cannot be migrated.
        -   Ensure that the name of an object is unique after it is migrated to the destination cluster. To change the name of an object before it is migrated the destination instance, move the pointer over the object in the Selected section, and then click **Edit**.
10. Click **Precheck**. After the precheck is successful, click **Next**.

    If the precheck fails, you can click the Info icon in the Result column of each failed item to view the details. Fix the problems as instructed and run the precheck again.

11. Confirm your DTS order information, read the **Data Transmission Service \(Pay-As-You-Go\) Service Terms**, select the check box to agree to them, and then click **Buy and Start Now**.

    **Note:** This migration service is free of charge.

12. Select the destination region to view the migration status. The status changes to **Completed** when the migration is completed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17772/15663535849779_en-US.png)


