# Migrate a POLARDB for MySQL cluster from beta to commercial releases {#concept_hwb_wpk_xdb .concept}

This topic describes how to migrate a POLARDB cluster from beta to commercial releases by using [Data Transmission Service \(DTS\)](https://www.alibabacloud.com/help/product/26590.htm). This migration service is free of charge.

## Prerequisites {#section_e5z_1rk_xdb .section}

**Configure whitelists**

Before the migration, you must follow these steps to configure a whitelist for the source and destination POLARDB clusters separately:

1.  Log on to the [POLARDB console](https://polardb.console.aliyun.com/).
2.  Find the target POLARDB cluster and click its ID.
3.  In the **Access Information** section of the Basics page, click **Create Whitelist** next to **Whitelists**. In the displayed dialog box, add the address **0.0.0.0/0** to allow all IP addresses to access this cluster.

**Note:** After the migration is complete, we recommend that you remove the IP address **0.0.0.0/0** from the whitelists of the source and destination POLARDB clusters.

**Create accounts**

Before the migration, you must create an account for the source and destination POLARDB clusters separately. The account can be a superuser account. For more information, see [Create an initial account for a POLARDB cluster](intl.en-US/Quick Start for MySQL/Create accounts for a POLARDB for MySQL cluster.md#).

**Stop write operations**

For data consistency purposes, you must stop writing data into the source POLARDB cluster before the migration starts.

## Procedure {#section_yww_nrk_xdb .section}

1.  Log on to the [DTS console](https://dts.console.aliyun.com/).
2.  In the left-side navigation pane, click **Data Migration**. Then in the upper-right corner, and click **Create Migration Task**.

    ![数据迁移](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13787/15665303243682_en-US.png)

3.  \(Optional\) Enter the task name.

    DTS automatically generates a name for each task. The name does not need to be unique. You can change the name as needed. An informative name is recommended for easier task identification.

4.  Set the following parameters for the source and destination POLARDB databases:

    -   **Instance Type**: Select **User-Created Database with Public IP Address**.
    -   **Instance Region**: Select the region where the POLARDB cluster is located.
    -   **Database Type**: Select **MySQL**.
    -   **Hostname or IP Address**: Enter the public connection endpoint for accessing the POLARDB cluster. For more information, see [View connection endpoints](intl.en-US/Quick Start for MySQL/View connection endpoints.md#).
    -   **Port Number**: Enter **3306**.
    -   **Database Account**: Enter the username of the superuser account for the POLARDB cluster.
    -   **Database Password**: Enter the password of the superuser account for the POLARDB cluster.
    ![设置迁移任务参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13787/15665303243683_en-US.png)

5.  In the lower-right corner, click **Set Whitelist and Next**.
6.  Select migration types and migration objects.
    -   **Migration Types**: Select **Schema Migration** and **Full Data Migration**.

        **Note:** Currently, DTS does not support **Incremental Data Migration**.

        -   **Schema Migration** 

            DTS migrates the schemas of tables from the source to the destination POLARDB clusters. DTS does not support the other objects such as views, synonyms, triggers, stored procedures, stored functions, packages, and user-defined data types.

        -   **Full Data Migration** 

            DTS migrates all existing data of the specified objects from the source to the destination POLARDB clusters.

    -   Migration objects: In the **Available** section, select the objects you want to migrate. Then, click the right arrow to move the selected objects to the **Selected** section.

        **Note:** 

        -   Migration of system tables is currently unavailable.
        -   The destination POLARDB cluster cannot have an object whose name is the same as the name of an object to be migrated. You can move the pointer over an object in the **Selected** section and then click **Edit** to change the object name.
7.  In the lower-right corner, click **Precheck**.

    If the migration task fails the precheck, you can click the **Result** button next to each failed item to view details. Rectify the faults accordingly, and perform the precheck again.

8.  Confirm the DTS order, select **Data Transmission Service \(Pay-As-You-Go\) Service Terms**, and then click **Buy and Start**.
9.  Click the target region to view the migration status. The status is displayed as **Completed** when the migration is completed.

