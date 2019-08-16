# Clone a cluster {#concept_sr2_x2f_v2b .concept}

You can create a ApsaraDB for POLARDB cluster the same as an existing ApsaraDB for POLARDB cluster by cloning the data of the existing one. The data includes the account information, but excludes parameter settings of the cluster.

The data generated before the execution of the clone action is cloned. When cloning starts, the newly written data will not be cloned.

## Procedure {#section_hxg_y52_v2b .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select the region where the target cluster is located.
3.  Find the cluster you want to clone. In the Actions column of the cluster, click the **More** icon, and then select **Restore to New Cluster**.
4.  On the page that appears, set the parameters. The following table describes the parameters.

    |Parameter|Description|
    |:--------|:----------|
    |Clone Source Type|The type of the clone source. Select **Current Cluster**.|
    |Region|The region where the cluster resides. The region of the new cluster is the same as that of the source cluster and cannot be modified.|
    |Primary Availability Zone|     -   The zone of the new cluster. A zone is an independent physical area located within a region. There are no substantive differences between the zones.
    -   You can deploy the ApsaraDB for POLARDB cluster and ECS instance in the same zone or in different zones.
 |
    |Network Type|     -   The type of the network. Use the default setting.
    -   ApsaraDB for POLARDB supports Virtual Private Cloud \(VPC\) networks only. A VPC is an isolated virtual network with higher security and performance than a classic network.
 |
    |VPC Vswitch

 |The VPC and VSwitch of the new cluster. Select a VPC and a VSwitch from the corresponding drop-down lists, or [create a VPC and a VSwitch](https://vpc.console.aliyun.com). **Note:** Make sure that you place your ApsaraDB for POLARDB cluster and the ECS instance to be connected in the same VPC. Otherwise, they cannot intercommunicate through the internal network and achieve optimal performance.

 |
    |Database Engine|The database engine of the new cluster. Use the default setting.|
    |Node Specification|The node specification of the new cluster. Select a specification according to your needs. Clusters with different specifications have different storage capacity and performance. For more information, see [Specifications and pricing](../../../../intl.en-US/Pricing/Specifications and pricing.md#).|
    |Number Nodes|The number of nodes in the new cluster. Use the default setting. By default, the system creates a read-only node with the same specification as the primary node.|
    |Cluster Name|     -   Optional. The name of the new cluster.
    -   The system will automatically create a name for your ApsaraDB for POLARDB cluster if you leave it blank. You can rename the cluster after it is created.
 |
    |Purchase Plan|The subscription duration of the new cluster. This parameter is valid only for subscription clusters.|
    |Number|The number of clusters. The default value 1 is used and cannot be modified.|

5.  Read the **ApsaraDB for POLARDB Agreement of Service**, select the check box to agree to it, and then complete the payment.

