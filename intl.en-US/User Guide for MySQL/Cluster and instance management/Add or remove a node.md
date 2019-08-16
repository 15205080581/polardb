# Add or remove a node {#concept_hc5_1yf_xdb .concept}

You can manually add or remove read-only nodes after creating an ApsaraDB for POLARDB cluster. An ApsaraDB for POLARDB cluster can contain a maximum of 15 read-only nodes. The cluster must have at least one read-only node to ensure high availability. All nodes in a cluster have the same specifications.

## Impact of the node quantity on performance {#section_cru_q2g_5gk .section}

For more information, see the [POLARDB for MySQL performance white paper](../../../../intl.en-US/Performance White Paper/Performance white paper.md#image_spr_wgj_h2b).

## Node cost {#section_1td_0zq_p6k .section}

The billing methods for adding nodes are as follows:

-   If the cluster is charged in subscription mode, the added nodes are also charged in this mode.
-   If the cluster is charged in pay-as-you-go mode \(hourly rate\), the added nodes are also charged in this mode.

**Note:** 

-   The read-only nodes that you purchase in either subscription or pay-as-you-go mode can be released at any time. After they are released, the system will [refund or stop billing](../../../../intl.en-US/Pricing/Configuration change fees.md#).
-   The added nodes are only charged based on the node specifications. For more information, see [Specifications and pricing](../../../../intl.en-US/Pricing/Specifications and pricing.md#). The storage fee is charged based on the actual data volume, regardless of the number of nodes.

## Important notes {#section_wbj_c3d_lfb .section}

-   You can add or remove read-only nodes only when the cluster does not have pending configuration change orders.
-   To avoid misoperations, only one read-only node can be added or removed at a time. You need to repeat the same operations to add or remove multiple nodes.
-   It takes about 5 minutes for the added or removed node to take effect.

## Add a read-only node {#section_zb3_yhd_lfb .section}

**Note:** After a read-only node is added, the newly created read-write splitting connection forwards requests to the node. The read-write splitting connection created before the new read-only node is added does not forward requests to the new read-only node. You need to disconnect and then re-establish the connection. For example, you can restart the application.

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Go to the Add/Remove Node page by using either of the following methods:
    -   Find the target cluster and click **Add/Remove Node** in the **Actions** column.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13773/156595003234661_en-US.png)

    -   Find the target cluster, click the cluster ID, and then click **Add/Remove Node** in the Node Information section.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13773/156595003313618_en-US.png)

4.  Select **Add Node** and click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13773/156595003352240_en-US.png)

5.  Click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13773/15659500333597_en-US.jpg) to add a read-only node. Read and agree to the service agreement by selecting the check box, and click **Pay** to complete the payment.

## Remove a read-only node {#section_fkk_13d_lfb .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Go to the Add/Remove Node page by using either of the following methods:
    -   Find the target cluster and click **Add/Remove Node** in the **Actions** column.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13773/156595003234661_en-US.png)

    -   Find the target cluster, click the cluster ID, and then click **Add/Remove Node** in the Node Information section.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13773/156595003313618_en-US.png)

4.  Select **Remove Node** and click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13773/156595003352249_en-US.png)

5.  Click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13773/15659500343601_en-US.png) next to the node that you want to remove. In the dialog box that appears, click **OK**.

    **Note:** You must keep at least one read-only node in the cluster to ensure high availability.

6.  Read and agree to the service agreement by selecting the check box, and click **OK**.

## Related API operations {#section_jbv_dpc_aly .section}

|API operation|Description|
|:------------|:----------|
|[CreateDBNodes](../../../../intl.en-US/API Reference/Node management/CreateDBNodes.md#)|Adds a node to an ApsaraDB for POLARDB cluster.|
|[ModifyDBNodeClass](../../../../intl.en-US/API Reference/Node management/ModifyDBNodeClass.md#)|Changes the specifications of a node in an ApsaraDB for POLARDB cluster.|
|[RestartDBNode](../../../../intl.en-US/API Reference/Node management/RestartDBNode.md#)|Restarts a node in an ApsaraDB for POLARDB cluster.|
|[DeleteDBNodes](../../../../intl.en-US/API Reference/Node management/DeleteDBNodes.md#)|Removes a node from an ApsaraDB for POLARDB cluster.|

