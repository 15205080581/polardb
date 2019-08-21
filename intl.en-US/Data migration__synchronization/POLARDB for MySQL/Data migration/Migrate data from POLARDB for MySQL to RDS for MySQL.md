# Migrate data from POLARDB for MySQL to RDS for MySQL {#concept_fvw_kpf_1hb .concept}

This topic describes how to migrate data from POLARDB for MySQL to RDS for MySQL by using Alibaba Cloud [Data Transmission Service \(DTS\)](https://www.alibabacloud.com/help/doc-detail/26592.htm).

## Preparations before migration {#section_zsh_m1h_1hb .section}

-   **Set an IP address whitelist for the source cluster** 

    Before data migration, you need to [set a whitelist](../../../../intl.en-US/Quick Start for MySQL/Configure a whitelist.md#) for the POLARDB for MySQL cluster, and add the Classless Inter-Domain Routing \(CIDR\) block of DTS to the whitelist.

    **Note:** You only need to add the [DTS CIDR block](https://www.alibabacloud.com/help/doc-detail/84900.htm) corresponding to the region where the destination database resides. In this example, the destination database is located in Hangzhou. You only need to add the DTS CIDR block corresponding to China \(Hangzhou\) to the whitelist.

-   **Create migration accounts** 

    When configuring a migration task, you need to provide the migration accounts for the POLARDB for MySQL cluster and the RDS for MySQL instance. If you have not created the migration accounts, create [an account for POLARDB for MySQL](intl.en-US/Quick Start for MySQL/Create an initial account for a POLARDB cluster.md) and [an account for RDS for MySQL](https://www.alibabacloud.com/help/doc-detail/87038.htm). First, create a migration account for the POLARDB for MySQL cluster and RDS for MySQL instance respectively. Then, grant the created accounts the permissions to read data from and write data to the tables or databases to be migrated.


## Migration permission requirements {#section_gmj_3tm_4gb .section}

When DTS is used to migrate data from **POLARDB for MySQL** to **RDS for MySQL**, the required permissions of the migration accounts on the source cluster and destination instance vary depending on the migration types. The following table lists the migration types and required permissions.

|Database type|Schema migration|Full data migration|
|-------------|----------------|-------------------|
|POLARDB for MySQL cluster|Read-only permissions|Read-only permissions|
|RDS for MySQL instance|Read and write permissions|Read and write permissions|

## Precautions {#section_c2v_xfg_chb .section}

-   POLARDB for MySQL does not support incremental data migration.
-   To ensure data consistency during migration, stop writing data to the POLARDB for MySQL cluster before the migration starts.
-   To ensure successful migration, the available storage of the RDS for MySQL instance must be larger than the used storage of the POLARDB for MySQL cluster.

## Procedure {#section_tvx_5bh_1hb .section}

1.  Log on to the [DTS console](https://dts.console.aliyun.com/).
2.  Click **Data Migration** in the left-side navigation pane, and then click **Create Migration Task** in the upper-right corner.
3.  Configure information about the source and destination databases. The following table describes the parameters.

    |Database type|Parameter|Description|
    |-------------|---------|-----------|
    |Source database|Instance Type|The type of the source database instance. Select **User-Created Database with Public IP Address**.|
    |Instance Region|The region where the POLARDB for MySQL cluster resides.|
    |Database Type|The type of the source database. Select **MySQL**.|
    |Hostname or IP Address|The public connection point of the POLARDB for MySQL cluster. For more information, see [View the connection point](../../../../intl.en-US/Quick Start for MySQL/View database connection strings.md#).|
    |Port Number|The listening port of the POLARDB for MySQL cluster. Default value: 3306.|
    |Database Account|The account for accessing the POLARDB for MySQL cluster.|
    |Database Password|The password of the account for accessing the POLARDB for MySQL cluster.|
    |Destination database|Instance Type|The type of the destination database instance. Select **RDS Instance**.|
    |Instance Region|The region where the RDS for MySQL instance resides.|
    |RDS Instance ID|The ID of the RDS for MySQL instance.|
    |Database Account|The account with the read and write permissions on the destination instance.|
    |Database Password|The password of the account for accessing the destination instance.|
    |Encryption|The encryption mode for accessing the destination instance. Select **Non-encrypted** or **SSL-encrypted**. The latter greatly increases CPU consumption. **Note:** Select SSL-encrypted only for the instances that have enabled [SSL encryption](https://help.aliyun.com/document_detail/96120.html).

 |

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136115/156636973640347_en-US.png)

4.  Click **Test Connectivity**. Ensure that both the source and destination databases pass the test.
5.  Click **Set Whitelist and Next**.
6.  Select the migration types and migration objects.******** 

    -   **Migration types**: Select **Schema Migration** and **Full Data Migration**. \(Currently, incremental data migration is not supported.\) To ensure data consistency during migration, stop writing data to the POLARDB for MySQL cluster before the migration starts.
        -   Schema migration:

            DTS migrates the schema definitions of the migration objects to the destination instance. Currently, DTS supports schema migration only for tables. For other objects such as views, synonyms, triggers, stored procedures, stored functions, packages, and user-defined data types, schema migration is not supported.

        -   Full data migration:

            DTS migrates all data of the migration objects to the destination instance.

    -   **Migration objects**: Select the objects to be migrated in the Available section, and then click the right arrow to add them to the Selected section.

        **Note:** 

        -   Currently, system tables cannot be migrated.
        -   Ensure that the name of an object is unique after it is migrated to the destination instance. To change the name of an object before it is migrated the destination instance, move the pointer over the object in the Selected section, and then click **Edit**.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136115/156636973740349_en-US.png)

7.  Click **Precheck** and wait until the precheck ends.

    **Note:** If the precheck fails, you can fix the problems as instructed and run the precheck again.

8.  Click **Next**. In the **Confirm Settings** dialog box that appears, read the **Data Transmission Service \(Pay-As-You-Go\) Service Terms**, select the check box to agree to them, and then click **Buy and Start**.

    **Note:** Currently, schema migration and full data migration tasks are free of charge.

9.  Select the destination region to view the migration status. The status changes to **Finished** when the migration is completed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136115/156636973740351_en-US.png)


