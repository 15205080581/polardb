# Automatically renew the subscription to a cluster {#concept_262454 .concept}

A subscription-based cluster has a validity period. If the cluster is not renewed in a timely manner, service interruptions or even data loss will occur after it expires. If you enable automatic renewal, you will be free from regular manual renewal operations and concerns of service interruptions.

**Note:** Clusters purchased through the pay-as-you-go \(hourly rate\) billing method do not involve expiration and renewal.

## Precautions {#section_wtz_qjn_wdb .section}

-   Automatic fee deduction will begin nine days prior to the expiration of the cluster, supporting cash and coupons. Keep your account balance adequate.
-   If you manually renew the cluster before the automatic deduction, the system will automatically renew the cluster nine days prior to the next expiration.
-   The automatic renewal feature takes effect the next day after it is enabled. If your cluster expires the next day, renew it manually to prevent service interruptions. For more information, see [Manually renew the subscription to a cluster](intl.en-US/User Guide for MySQL/Billing management/Manually renew the subscription to a cluster.md#).

## Enable automatic renewal when purchasing a cluster {#section_05j_6cb_1j9 .section}

**Note:** After you enable automatic renewal, the system will automatically renew the subscription based on the **subscription period**. For example, if you purchase a cluster for three months and select automatic renewal, you will be charged a fee of the three-month subscription upon each automatic renewal.

When creating a cluster, you can select **Auto Renew**.

![Enable automatic renewal when purchasing a cluster](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216851/156698575946767_en-US.png)

## Enable automatic renewal after purchasing a cluster {#section_646_x4z_eov .section}

**Note:** After you enable automatic renewal, the system will automatically renew the subscription based on the renewal cycle you select. For example, if you select a three-month renewal cycle, you will be charged a fee of the three-month subscription upon each automatic renewal.

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  In the upper-right corner of the console, choose **Billing Management** \> **Renew**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3030/156698575956597_en-US.png)

3.  In the left-side navigation pane, click **ApsaraDB for POLARDB**.
4.  Click the Manually Renew or Don't Renew tab on the Renew console. Set the filtering conditions to find the target cluster. Click **Enable Auto-Renew** in the Actions column corresponding to the cluster.
5.  In the dialog box that appears, select the ****automatic renewal cycle, and click **Enable Auto-Renew**.

    ![Enable automatic renewal](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216851/156698575946771_en-US.png)


## Edit the automatic renewal cycle {#section_la0_mn6_xtf .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  In the upper-right corner of the console, choose **Billing Management** \> **Renew**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3030/156698575956597_en-US.png)

3.  In the left-side navigation pane, click **ApsaraDB for POLARDB**.
4.  Click the Auto-Renew tab on the Renew console. Set the filtering conditions to find the target cluster. Click **Enable Auto-Renew** in the Actions column corresponding to the cluster.
5.  Click the Auto tab. Set the filtering conditions to find the target cluster. Click **Modify Auto-Renew** in the Actions column corresponding to the cluster.
6.  In the dialog box that appears, edit the automatic renewal cycle, and click **OK**.

## Disable automatic renewal {#section_mr7_sbp_685 .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  In the upper-right corner of the console, choose **Billing Management** \> **Renew**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3030/156698575956597_en-US.png)

3.  In the left-side navigation pane, click **ApsaraDB for POLARDB**.
4.  Click the Auto-Renew tab on the Renew console. Set the filtering conditions to find the target cluster. Click **Modify Auto-Renew** in the Actions column corresponding to the cluster.
5.  Select **Disable Auto-Renew** and click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216851/156698575956629_en-US.png)


## Related operations {#section_0kw_zsf_7q4 .section}

|Operation|Description|
|:--------|:----------|
|[CreateDBCluster](../../../../intl.en-US/API Reference/Cluster management/CreateDBCluster.md#)|Creates a POLARDB cluster. **Note:** You can enable automatic renewal when you create a cluster.

 |
|[ModifyAutoRenewAttribute](../../../../intl.en-US/API Reference/Cluster management/ModifyAutoRenewAttribute.md#)|Enables automatic renewal for a subscription-based cluster. **Note:** You can enable automatic renewal after you create a cluster.

 |
|[DescribeAutoRenewAttribute](../../../../intl.en-US/API Reference/Cluster management/DescribeAutoRenewAttribute.md#)|Queries the automatic renewal status of a subscription-based cluster.|

