# Configure a whitelist {#concept_ew4_wmq_tdb .concept}

After a cluster is created, you must add the IP addresses for accessing the cluster to a whitelist, and create an initial account. Otherwise, you cannot access or use this cluster.

Only IP addresses in the whitelist can be used to visit the instances in the cluster. The whitelist can only be configured in the cluster details page, and is applicable to all instances in the cluster.

**Note:** 

-   By default, the whitelist only contains an IP address 127.0.0.1. It means that no IP addresses can access the cluster.

-   If the whitelist is set to % or 0.0.0.0/0, it allows all IP addresses to access the cluster. This configuration substantially compromises the database security. Therefore, this configuration is not recommended.

-   POLARDB cannot automatically obtain internal IP addresses of ECS instances in the VPC. You must add the internal IP addresses to the whitelist.


## Procedure {#section_zxh_25y_k2b .section}

1.  Log on to the [POLARDB Console](https://polardb.console.aliyun.com).

2.  In the left-side navigation pane, click **Cluster List**, and find your target cluster.

3.  Click the cluster ID, or click **Manage** in the **Actions** column.

4.  In the **Access Information** section, click the icon ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/68506/cn_zh/1521975822343/28.png) next to the **Whitelist**.

5.  In the **Modify Whitelist** dialog box, add IP addresses to allow these addresses to access your cluster.

6.  Click **OK**.


## Related documents {#section_h42_vlv_tdb .section}

[How to locate the local IP address using ApsaraDB for MySQL](https://help.aliyun.com/document_detail/41754.html)

