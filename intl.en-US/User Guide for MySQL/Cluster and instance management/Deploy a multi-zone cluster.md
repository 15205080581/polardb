# Deploy a multi-zone cluster {#concept_694842 .concept}

POLARDB for MySQL supports deploying a cluster across multiple zones. Compared with single-zone clusters, multi-zone clusters have better disaster recovery capabilities and can withstand breakdowns in a data center.

## Multi-zone architecture {#section_n1v_ous_pgb .section}

When a multi-zone cluster is deployed, data is distributed across multiple zones. Currently, compute nodes must be deployed in the primary zone. ApsaraDB for POLARDB reserves sufficient resources in a secondary zone to ensure a successful failover when the primary zone fails. The following figure shows the multi-zone architecture.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/557535/156645571049457_en-US.png)

## Pricing {#section_1pp_mb9_u4m .section}

No additional fee is required for multi-zone deployment.

**Note:** You can also upgrade a single-zone cluster to a multi-zone cluster for free.

## Prerequisites {#section_buw_gy9_ox8 .section}

-   The cluster resides in China \(Hangzhou\) or China \(Zhangjiakou\).
-   There are at least two zones with sufficient computing resources in the region.

## Establish the multi-zone architecture {#section_1ua_xe8_h02 .section}

When the [prerequisites](#) are met, the cluster you [create](../../../../intl.en-US/Quick Start for MySQL/Create a POLARDB cluster.md#) is set as a multi-zone cluster by default.

You can also upgrade the existing single-zone clusters to multi-zone ones. This upgrade is automatically completed through online data migration without affecting your business.

![Select the primary zone when creating a cluster.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/557535/156645571149461_en-US.png)

## View the zones of a cluster {#section_eoc_b5u_3qm .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Find the target cluster and click the cluster ID in the **Cluster Name** column.
4.  In the Basic Information section on the Basics page, view the zones of the cluster listed in **Zones**.

    ![Zones](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/557535/156645571149462_en-US.png)


