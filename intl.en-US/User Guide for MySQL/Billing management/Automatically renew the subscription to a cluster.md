# Automatically renew the subscription to a cluster {#concept_262454 .concept}

A subscription-based cluster has a validity period. If the cluster is not renewed in a timely manner, service interruptions or even data loss will occur after it expires. If you enable automatic renewal, you will be free from regular manual renewal operations and concerns of service interruptions.

**Note:** Clusters purchased through the pay-as-you-go \(hourly rate\) billing method do not involve expiration and renewal.

## Important notes {#section_wtz_qjn_wdb .section}

-   Automatic fee deduction will begin nine days prior to the expiration of the cluster, supporting cash and coupons. Please keep your account balance adequate.
-   If you manually renew the cluster before the automatic deduction, the system will automatically renew the cluster nine days prior to the next expiration.
-   The automatic renewal function takes effect the next day after it is enabled. If your cluster expires the next day, renew it manually to prevent service interruptions. For more information, see [Manually renew the subscription to a cluster](intl.en-US/User Guide for MySQL/Billing management/Manually renew the subscription to a cluster.md#).

## Enable automatic renewal {#section_grh_sjn_wdb .section}

**Enable automatic renewal when purchasing a cluster**

**Note:** After you enable automatic renewal, the system will automatically renew the subscription based on the **subscription period**. For example, if you purchase a cluster for three months and select automatic renewal, you will be charged a fee of the three-month subscription upon each automatic renewal.

When creating a cluster, you can select **Automatic Renewal**.

![Enable automatic renewal when purchasing a cluster](images/46767_en-US.png)

**Enable automatic renewal after purchasing a cluster**

**Note:** After you enable automatic renewal, the system will automatically renew the subscription based on the renewal cycle you select. For example, if you select a three-month renewal cycle, you will be charged a fee of the three-month subscription upon each automatic renewal.

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  In the upper-right corner of the console, choose **Billing Management** \> **Renew**.

    ![Go to the Renew page](images/46768_en-US.png)

3.  Click **Experience New Version** in the upper-left corner of the console to switch to the new version.

    ![Switch to the new version](images/48373_en-US.png)

4.  Click the Manual or Nonrenewal tab on the Renew page. Set the filter conditions to find the target clusters. You can enable automatic renewal for a single cluster or multiple clusters at a time.
    -   **Enable automatic renewal for a single cluster** 
        1.  Click **Enable Automatic Renewal** on the right side.

            ![Enable automatic renewal after purchasing a cluster](images/46770_en-US.png)

            **Note:** The example demonstrates the procedure in the new version of the Renew console. If you want to use the previous version, choose **ApsaraDB for POLARDB** in the left-side navigation pane, and enable automatic renewal on the page that appears.

        2.  In the dialog box that appears, select the **automatic renewal cycle**, and click **Enable Automatic Renewal**.

            ![Enable automatic renewal](images/46771_en-US.png)

    -   **Enable automatic renewal for multiple clusters** 

        Select the target clusters and click **Enable Automatic Renewal** below.

        ![Enable automatic renewal for multiple clusters](images/48385_en-US.png)

    -   In the dialog box that appears, select the **automatic renewal cycle**, and click **Enable Automatic Renewal**.

        ![](images/48386_en-US.png)


## Modify automatic renewal settings {#section_d2g_wcy_s2b .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  In the upper-right corner of the console, choose **Billing Management** \> **Renew**.

    ![Go to the Renew page](images/46768_en-US.png)

3.  Click **Experience New Version** in the upper-left corner of the console to switch to the new version.
4.  Click the Auto tab on the Renew page. Set the filter conditions to find the target cluster. Click **Modify Automatic Renewal Settings** on the right side.

    ![Modify automatic renewal settings](images/46773_en-US.png)

    **Note:** The example demonstrates the procedure in the new version of the Renew console. If you want to use the previous version, choose **ApsaraDB for POLARDB** in the left-side navigation pane, and modify automatic renewal settings on the page that appears.

5.  In the dialog box that appears, modify the automatic renewal cycle, and click **OK**.

## Disable automatic renewal {#section_nxd_hih_n1m .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  In the upper-right corner of the console, choose **Billing Management** \> **Renew**.

    ![Go to the Renew page](images/46768_en-US.png)

3.  Click **Experience New Version** in the upper-left corner of the console to switch to the new version.
4.  Click the Auto tab on the Renew page. Set the filter conditions to find the target cluster. Click **Resume Manual Renewal** on the right side.

    ![Disable automatic renewal](images/48390_en-US.png)

    **Note:** The example demonstrates the procedure in the new version of the Renew console. If you want to use the previous version, choose **ApsaraDB for POLARDB** in the left-side navigation pane, and disable automatic renewal on the page that appears.

5.  In the dialog box that appears, click **OK**.

## Related API operations {#section_0kw_zsf_7q4 .section}

|API operation|Description|
|:------------|:----------|
|[CreateDBCluster](../../../../intl.en-US/API Reference/Cluster management/CreateDBCluster.md#)|Creates an ApsaraDB for POLARDB cluster. **Note:** You can enable automatic renewal when you purchase a cluster.

 |
|[ModifyAutoRenewAttribute](../../../../intl.en-US/API Reference/Cluster management/ModifyAutoRenewAttribute.md#)|Enables automatic renewal for a subscription-based cluster. **Note:** You can enable automatic renewal after a cluster is purchased.

 |
|[DescribeAutoRenewAttribute](../../../../intl.en-US/API Reference/Cluster management/DescribeAutoRenewAttribute.md#)|Queries the automatic renewal status of a subscription-based cluster.|

