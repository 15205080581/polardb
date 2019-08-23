# Set a maintenance window {#concept_lfd_2cd_2gb .concept}

To ensure the stability of ApsaraDB for POLARDB, the backend system performs maintenance operations on the clusters from time to time. We recommend that you set the maintenance window within the off-peak hours of your business to minimize the impact on the business during the maintenance process.

## Important notes {#section_slc_mcd_2gb .section}

-   Before the maintenance is performed, ApsaraDB for POLARDB sends SMS messages and emails to contacts listed in your Alibaba Cloud account.
-   To ensure stability during the maintenance process, clusters first enter the **Under Maintenance** status before the preset maintenance window arrives on the day of maintenance. When a cluster is in this status, **normal data access to the database is not affected**. However, except for the **account management**, **database management**, and **IP address whitelisting** functions, other services concerning changes \(such as common operations like upgrade, degrade, and restart\) are unavailable in the console of this cluster. **Query services such as performance monitoring are still available.**
-   Within the maintenance window of a cluster, the cluster may experience one or two disconnections. Make sure that your application has an automatic reconnection mechanism. The cluster restores to the normal status immediately after the disconnection occurs.

## Procedure {#section_nhn_mrt_g2b .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com).
2.  Select a region.
3.  Find the target cluster and click the cluster ID in the **Cluster Name** column.
4.  In the Basic Information section on the Basics page, click **Modify** next to **Maintenance Window**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/80668/156594107034528_en-US.png)

5.  In the **Modify Maintenance Window** dialog box that appears, select a maintenance window for the cluster and click **Submit**.

## Related API operations {#section_arh_n4h_yfb .section}

|API operation|Description|
|:------------|:----------|
|[CreateDBCluster](intl.en-US/API Reference/Cluster management/CreateDBCluster.md#)|Creates an ApsaraDB for POLARDB cluster.|
|[ModifyDBClusterMaintainTime](intl.en-US/API Reference/Cluster management/ModifyDBClusterMaintainTime.md#)|Modifies the maintenance window for an ApsaraDB for POLARDB cluster.|

