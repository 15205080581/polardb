# Back up data {#concept_yfg_vzf_xdb .concept}

ApsaraDB for POLARDB uses a physical backup \(snapshot backup\), which is automatically performed once a day. You can also manually start a backup. Both the automatic backup and manual backup do not affect the normal running of the cluster. Backup files are retained for seven days.

## Backup types {#section_rhc_jrf_v2b .section}

|Backup type|Description|
|-----------|-----------|
|Automatic backup| -   It is performed once a day by default. You can configure the time period and cycle for an automatic backup. For more information, see [Configure an automatic backup](#).
-   Backup files cannot be deleted.

 |
|Manual backup| -   It can be started at any time. You can create a maximum of three manual backups for a cluster. For more information, see [Create a manual backup](#).
-   Backup files can be deleted.

 |

## Pricing {#section_mbm_r4f_v2b .section}

Currently, the storage occupied by ApsaraDB for POLARDB backup files is free of charge.

## Configure an automatic backup {#section_ebx_rpf_v2b .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Find the target cluster and click the cluster ID in the **Cluster Name** column.
4.  In the left-side navigation pane, choose **Settings and Management** \> **Backup and Restore**.
5.  Click **Backup Settings**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13774/156593891311827_en-US.png)

6.  In the dialog box that appears, configure the time period and cycle for an automatic backup.

    **Note:** For security reasons, an automatic backup must be performed at least twice a week.


## Create a manual backup {#section_gzn_byx_ydb .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Find the target cluster and click the cluster ID in the **Cluster Name** column.
4.  In the left-side navigation pane, choose **Settings and Management** \> **Backup and Restore**.
5.  Click **Create Backup**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13774/156593891311857_en-US.png)

6.  In the dialog box that appears, click **OK**.

    **Note:** You can create a maximum of three manual backups for a cluster.


## Restore data {#section_tyv_cwt_v2b .section}

For more information, see [Restore data](intl.en-US/User Guide for MySQL/Backup and restore/Restore data.md).

