# Restore data {#concept_xb3_dlz_52b .concept}

The process of restoring data of a POLARDB for MySQL cluster is as follows:

1.  Restore historical data to a new cluster. You can choose either of the following methods to restore data:
    -   [Restore data to a specific point in time.](#)
    -   [Restore data from a backup set \(snapshot\).](#)
2.  [Log on to the new cluster](../../../../intl.en-US/User Guide for MySQL/Connect to POLARDB/Connect to a POLARDB for MySQL cluster.md) and verify the data accuracy.

**Note:** The restored cluster data contains the data and account information of the original cluster, excluding the parameter settings of the original cluster.

## Restore data to a specific point in time {#section_hxg_y52_v2b .section}

You can restore data to **a specific point in time** in the last seven days in a new cluster.

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select the region where the original cluster resides.
3.  Find the target cluster and click the cluster ID in the Cluster Name column.
4.  In the left-side navigation pane, choose **Settings and Management** \> **Backup and Restore**.
5.  Click **Point-in-time Restore**. In the dialog box that appears, click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17710/156878866334703_en-US.png)

6.  On the Clone Instance page, select a billing method for the new cluster:
    -   **Subscription**: For the new cluster created, you need to pay the subscription fee for a compute cluster \(with a primary node and a read-only node by default\). The storage occupied by the new cluster is billed on an hourly basis based on the actual data volume. The payment will be deducted from your Alibaba Cloud account on an hourly basis. The **subscription** method is more cost-effective if you want to use the new cluster for a long term. You can save more with longer subscription periods.
    -   **Pay-As-You-Go \(Hourly Rate\)**: For the new cluster created, you do not need to pay any subscription fee for a compute cluster in advance. Use of the compute cluster is billed on an hourly basis. The storage occupied by the new cluster is billed on an hourly basis based on the actual data volume. The payment will be deducted from your Alibaba Cloud account on an hourly basis. The **pay-as-you-go** method is suitable if you only want to use the new cluster for a short term. You can save the cost by releasing the cluster as soon as you complete the data restore.
7.  Set the following parameters:
    -   **Clone Source Type**: Select **Backup Timepoint**.
    -   **Backup Timepoint**: Set it to a specific point in time in the last seven days.
    -   **Region**: It is the same as the region of the original cluster. Use the default setting.
    -   **Primary Availability Zone**: Use the default setting.
    -   **Network Type**: Use the default setting.
    -   **VPC** and **Vswitch**: We recommend that you use the default settings, namely, the VPC and VSwitch of the original cluster.
    -   **Database Engine**: Use the default setting.
    -   **Node Specification**: Clusters with different specifications have different storage capacity and performance. For more information, see [Specifications and pricing](../../../../intl.en-US/Pricing/Specifications and pricing.md#).
    -   **Number Nodes**: Use the default setting. By default, the system will create a read-only node with the same specifications as the primary node.
    -   **Cluster Name**: The system will automatically create a name for your POLARDB cluster if you leave it blank. You can rename the cluster after it is created.
    -   **Purchase Plan**: Set this parameter if you create a cluster in subscription mode.
    -   **Number**: The default value is 1, which cannot be modified.
8.  Read and agree to the **ApsaraDB for POLARDB service agreement** by selecting the check box, and then complete the payment.

## Restore data from a backup set \(snapshot\) {#section_yvd_vdf_v2b .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select the region where the original cluster resides.
3.  Find the target cluster and click the cluster ID in the Cluster Name column.
4.  In the left-side navigation pane, choose **Settings and Management** \> **Backup and Restore**.
5.  Find the target backup set \(snapshot\) and click **Restore** in the Actions column. In the dialog box that appears, click **OK**.
6.  On the page that appears, select a billing method for the new cluster:
    -   **Subscription**: For the new cluster created, you need to pay the subscription fee for a compute cluster \(with a primary node and a read-only node by default\). The storage occupied by the new cluster is billed on an hourly basis based on the actual data volume. The payment will be deducted from your Alibaba Cloud account on an hourly basis. The **subscription** method is more cost-effective if you want to use the new cluster for a long term. You can save more with longer subscription periods.
    -   **Pay-As-You-Go**: For the new cluster created, you do not need to pay any subscription fee for a compute cluster in advance. Use of the compute cluster is billed on an hourly basis. The storage occupied by the new cluster is billed on an hourly basis based on the actual data volume. The payment will be deducted from your Alibaba Cloud account on an hourly basis. The **pay-as-you-go** method is suitable if you only want to use the new cluster for a short term. You can save the cost by releasing the cluster as soon as you complete the data restore.
7.  Set the following parameters:
    -   **Clone Source Type**: Select **Backup Set**.
    -   **Clone Source Backup Set**: Confirm that the backup set is the one that you want to restore from.
    -   **Region**: It is the same as the region of the original cluster. Use the default setting.
    -   **Primary Availability Zone**: Use the default setting.
    -   **Network Type**: Use the default setting.
    -   **VPC** and **Vswitch**: We recommend that you use the default settings, namely, the VPC and VSwitch of the original cluster.
    -   **Database Engine**: Use the default setting.
    -   **Node Specification**: Clusters with different specifications have different storage capacity and performance. For more information, see [Node specifications](../../../../intl.en-US/Pricing/Specifications and pricing.md#).
    -   **Number Nodes**: Use the default setting. By default, the system will create a read-only node with the same specifications as the primary node.
    -   **Cluster Name**: The system will automatically create a name for your POLARDB cluster if you leave it blank. You can rename the cluster after it is created.
    -   **Purchase Plan**: Set this parameter if you create a cluster in subscription mode.
    -   **Number**: The default value is 1, which cannot be modified.
8.  Read and agree to the **ApsaraDB for POLARDB service agreement** by selecting the check box, and then complete the payment.

## FAQ {#section_rlc_yzk_qgb .section}

1.  Q: Does the point-in-time restore method depend on binlogs? Is it possible to restore data to any point in time in the retention period of binlogs?

    A: The point-in-time restore method does not depend on binlogs. The cluster data can be restored to any point in time in the last seven days. The data restore is based on redo logs rather than binlogs.

2.  Q: Is the data restore based on a full backup plus binlogs?

    A: The data restore is based on a full snapshot backup plus redo logs.

    The size of redo logs depends on your database write load. If a database is frequently written or updated, a large number of redo logs are generated. The system regularly uploads redo logs, and then clears the local redo logs. The local redo logs temporarily occupy the storage of the cluster and cost you a certain amount of fees. You will not be charged for the local redo logs after they are uploaded.


## Related topics {#section_h21_1wt_v2b .section}

[Back up data](intl.en-US/User Guide for MySQL/Backup and restore/Back up data.md)

