# Configure a whitelist for a POLARDB for MySQL cluster {#concept_ew4_wmq_tdb .concept}

After a POLARDB cluster is created, you must add the IP addresses for accessing the cluster to a whitelist, and create an initial account. Otherwise, you cannot access or use the cluster.

Only IP addresses in the whitelist can be used to visit the nodes in the cluster. The whitelist can only be configured on the cluster details page, and is applicable to all nodes in the cluster.

## Precautions {#section_mj6_rbj_knn .section}

-   By default, the whitelist only contains an IP address **127.0.0.1**. It means that no IP addresses can access the cluster.
-   If the whitelist is set to **%** or **0.0.0.0/0**, it allows all IP addresses to access the cluster. This configuration substantially compromises the database security. Therefore, this configuration is not recommended.
-   POLARDB cannot automatically obtain the private IP addresses of ECS instances in the VPC. You must add the private IP addresses to the whitelist manually.

## Procedure {#section_zxh_25y_k2b .section}

1.  Log on to the [POLARDB console](https://polardb.console.aliyun.com).
2.  Find the target POLARDB cluster and click its ID.
3.  In the **Access Information** section of the Basics page, click **Configure** below **Whitelists**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3015/156652987113598_en-US.png)

4.  In the Configure Whitelist dialog box, add IP addresses to allow these IP addresses to access the POLARDB cluster.

5.  Click **Submit**.


## APIs {#section_5jy_o14_cvl .section}

|API|Description|
|:--|:----------|
|[DescribeDBClusterAccessWhiteList](../../../../intl.en-US/API Reference/Whitelist management/DescribeDBClusterAccessWhiteList.md#)|Used to list the IP address that are allowed to access the a POLARDB cluster.|
|[ModifyDBClusterAccessWhiteList](../../../../intl.en-US/API Reference/Whitelist management/ModifyDBClusterAccessWhiteList.md#)|Used to modify the list of IP addresses that are allowed to access the POLARDB cluster.|

