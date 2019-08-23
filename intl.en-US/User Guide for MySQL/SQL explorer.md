# SQL explorer {#concept_sfj_qqr_2gb .concept}

ApsaraDB for RDS provides the SQL explorer feature, so that you can perform security audit and performance diagnostics on your database.

## Pricing {#section_vjr_yct_2gb .section}

-   Trial edition: free to use. Audit logs are stored for only one day, that is, only data within one day can be queried. This edition does not support advanced features such as data export, and cannot guarantee data integrity.
-   Purchase 30 days or more: RMB 0.008 per GB per hour.

## Features {#section_ovx_hcv_lfb .section}

-   **SQL log**: records all actions that have been performed on databases. By using SQL logging, you can troubleshoot database failures, analyze actions, and perform security auditing.
-   **Enhanced search**: You can search data by database, user, client IP, thread ID, storage duration, or execution status, and then export and download the search results.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81394/156593889034838_en-US.png)

-   **SQL analysis**: allows you to analyze SQL log entries generated within the specified time period in a visualized and interactive way. You can use this feature to locate error SQL statements and performance issues.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81394/156593889034839_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81394/156593889134840_en-US.png)


## Enable the SQL explorer feature {#section_g4n_21b_mfb .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select the region where the target cluster is located.
3.  Find the target cluster, and then click the cluster ID in the Cluster Name column.****
4.  In the left-side navigation pane, choose **Log and Audit** \> **SQL Explorer**.
5.  Click **Activate Now**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81394/156593889134841_en-US.png)

6.  Select the storage duration of SQL logs, and then click **Activate**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81394/156593889134842_en-US.png)


## Modify the storage duration of SQL logs {#section_sgz_q13_mfb .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select the region where the target cluster is located.
3.  Find the target cluster, and then click the cluster ID in the Cluster Name column.****
4.  In the left-side navigation pane, choose **Log and Audit** \> **SQL Explorer**.
5.  Click **Service Settings** in the upper-right corner.
6.  Change the storage duration, and then click **OK**.

## Export SQL records {#section_f4b_sb3_mfb .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select the region where the target cluster is located.
3.  Find the target cluster, and then click the cluster ID in the Cluster Name column.****
4.  In the left-side navigation pane, choose **Log and Audit** \> **SQL Explorer**.
5.  Click **Export**.
6.  In the dialog box that appears, select the items to export and click **Ok**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81394/156593889134843_en-US.png)

7.  After the export process is completed, download the log files in the Export SQL Log Records dialog box.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81394/156593889134844_en-US.png)


## Disable the SQL explorer feature {#section_myx_gws_2gb .section}

**Note:** 

After the SQL explorer feature is disabled, the SQL logs will be cleared. [Export SQL logs](#) to your local disk before you disable the SQL explorer feature.

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select the region where the target cluster is located.
3.  Find the target cluster, and then click the cluster ID in the Cluster Name column.****
4.  In the left-side navigation pane, choose **Log and Audit** \> **SQL Explorer**.
5.  Click **Service Settings**.
6.  Turn off the Activate SQL Explorer switch.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81394/156593889134845_en-US.png)


## View the size and consumption details of audit logs {#section_ycb_ldv_ggb .section}

1.  Log on to the [Alibaba Cloud console](https://home.console.aliyun.com/new#/).
2.  In the upper-right corner of the page, choose **Billing Management** \> **Billing Management**.
3.  On the page that appears, choose **Purchases record** \> **Purchases details** in the left-side navigation pane.
4.  Click the **Cloud products** tab.

    ![](images/35495_en-US.png)

5.  Click the **Details of bill records** tab.
6.  Click **Post-payment**.
7.  Set query conditions, and then click **Query**.

    **Note:** If you need to query records generated more than 12 months ago, open a ticket.

8.  Find a record where the billing method is pay-as-you-go or subscription, and then click **Details** in the Actions column.********
9.  Click the arrow on the rightmost side to view the audit log size and cost of the SQL explorer feature.

    ![](images/35494_en-US.png)


