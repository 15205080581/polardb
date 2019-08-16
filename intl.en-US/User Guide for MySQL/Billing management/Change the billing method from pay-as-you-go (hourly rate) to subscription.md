# Change the billing method from pay-as-you-go \(hourly rate\) to subscription {#concept_plc_t5t_g2b .concept}

You can change the billing method of a cluster from pay-as-you-go \(hourly rate\) to subscription to meet your needs. Changing the billing method will not impact the performance of an ApsaraDB for POLARDB cluster.

**Note:** If a cluster uses a specification that is no longer available, you cannot change the billing method of the cluster to subscription. In this case, you need to [EN-US\_TP\_13772.md](intl.en-US/User Guide for MySQL/Cluster and instance management/Change specifications.md) before changing the billing method.

## Precautions {#section_fwc_jxt_g2b .section}

You cannot change the billing method of a cluster from subscription to pay-as-you-go \(hourly rate\). Exercise caution before you change the billing method to subscription.

## Prerequisites {#section_szp_y15_g2b .section}

-   The status of your cluster must be **Running**.
-   There are no pending orders for changing the billing method from pay-as-you-go \(hourly rate\) to subscription. If there are any pending orders, you must pay or discard them on the [Orders](https://expense.console.aliyun.com/#/order/list/) page.

## Procedure {#section_prv_z15_g2b .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com).
2.  Select the region where the cluster is located.
3.  Find the target cluster. In the **Actions** column of the cluster, click the **More** icon, and then select **Switch to Subscription**.

    ![](images/6580_en-US.png)

4.  Specify the renewal duration, read the ApsaraDB for POLARDB Subscription Agreement of Service, select the check box to agree to it, and then click **Activate**.********

    **Note:** 

    -   The new billing method will take effect after you complete the payment.
    -   If the order is unpaid or payment is unsuccessful, an incomplete order will be listed on the [Orders](https://expense.console.aliyun.com/#/order/list/) page, and you cannot purchase any new cluster or change the billing method to subscription. You must pay or discard the order before placing a new one.

