# Perform a temporary upgrade {#concept_944231 .concept}

For an ApsaraDB for POLARDB cluster you subscribed to, you can temporarily upgrade the specifications of the cluster to meet the business peak requirements in the specified validity period.

## Description {#section_nn9_1kw_a67 .section}

A temporary upgrade allows you to temporarily upgrade the specifications of an ApsaraDB for POLARDB cluster to improve overall performance. When the specified restore point is reached, the specifications of the cluster will be automatically restored to the status before the temporary upgrade.

**Note:** A temporary downgrade is not supported. For more information about downgrades, see [Change specifications](intl.en-US/User Guide for MySQL/Cluster and instance management/Change specifications.md#).

## Prerequisites {#section_zlj_qqa_ben .section}

-   The cluster is subscription-based.
-   The cluster has no pending renewal or configuration change orders.
-   The cluster has no pending temporary upgrade orders.

## Impact {#section_0ed_yhf_6xy .section}

Disconnections may occur during the configuration restore process. Make sure that your application has an automatic reconnection mechanism.

## Important notes {#section_a10_xr1_51d .section}

-   The restore point must be at least one day earlier than the expiration time of the cluster. For example, if a cluster expires on January 10, the restore point must be on January 9 at latest.
-   The minimum validity period for a temporary upgrade is one day. We recommend that you set the validity period to up to 14 days because the restore point cannot be changed after it is set.
-   Regular [configuration change](intl.en-US/User Guide for MySQL/Cluster and instance management/Change specifications.md#) methods are not supported during the temporary upgrade.
-   If the performance is still insufficient after the temporary upgrade, you can perform a maximum of one more temporary upgrade before the restore point is reached. The **restore point** that you set in this temporary upgrade cannot be earlier than the previous one.

## Pricing {#section_6lr_31k_lq6 .section}

The price of a temporary upgrade is 1.5 times the price difference between the original and new specifications. Assume that the validity period of the temporary upgrade is N days. The price of a temporary upgrade is calculated as follows:

Price = \(Monthly subscription fee for the new specifications - Monthly subscription fee for the original specifications\)/30 × 1.5 × N

## Perform a temporary upgrade {#section_lga_m1z_sbg .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Go to the Change Configurations page by using either of the following methods:
    -   Find the target cluster and click **Change Configurations** in the **Actions** column.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13772/156594065013607_en-US.png)

    -   Find the target cluster, click the cluster ID, and then click **Change Configurations** in the Node Information section.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13772/156594065034579_en-US.png)

4.  Select **Temporary Upgrade**, and click **OK**.

    **Note:** **Temporary Upgrade** is available only for subscription-based clusters.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/763549/156594065052266_en-US.png)

5.  Select the node specifications.
6.  Set **Restore Point**.

    **Note:** 

    -   If the performance is still insufficient after the **temporary upgrade**, you can perform a maximum of one more temporary upgrade before the restore point is reached. The **restore point** that you set in this temporary upgrade cannot be earlier than the previous one.
    -   The minimum validity period for a temporary upgrade is one day. We recommend that you set the validity period to up to 14 days because the restore point cannot be changed after it is set.
    -   The restore point must be at least one day earlier than the expiration time of the cluster.
    ![](images/50603_en-US.png)

7.  Read and agree to the service agreement by selecting the check box, and click **Pay** to complete the payment.

