# Clone a cluster

This topic describes how to create new PolarDB clusters by cloning the data of source PolarDB clusters.

## Considerations

-   The data that can be cloned includes:
    -   The account information about the source cluster.
    -   If Transparent Data Encryption \(TDE\) is enabled for the source cluster before you perform clone operations, the TDE configurations can also be cloned.
-   The data that cannot be cloned includes:
    -   The parameter settings of the source cluster.
    -   The whitelist configurations of the source cluster.
    -   The secure sockets layer \(SSL\) configurations of the source cluster.
-   Only the data that exists in the source cluster before the clone operation starts can be cloned. The data that is written to the source cluster after the clone operation starts cannot be cloned.

## Procedure

1.  Log on to the [PolarDB console](https://polardb.console.aliyun.com/).

2.  On the top of the page, select the region where the target cluster is located.

3.  Find the cluster that you want to clone. In the **Actions** column, choose **More** \> **Clone Cluster**.

4.  On the page that appears, specify the following parameters.

    |Parameter|Description|
    |:--------|:----------|
    |Clone Source Type|The type of the clone source. The default value is **Current Cluster**. Use the default setting.|
    |Region|The region where the cluster to be created resides. By default, the region of the new cluster is the same as that of the source cluster. For example, if the source cluster resides in the **China \(Hangzhou\)** region, the default region of the new cluster is also **China \(Hangzhou\)**. Use the default setting.|
    |Primary Availability Zone|    -   Each zone is an independent geographical location that resides in a region. The zones that are deployed in the same region are similar.
    -   You can deploy your PolarDB cluster and the Elastic Compute Service \(ECS\) instance to be connected in the same zone or in different zones. |
    |Network Type|The type of the network. The value of this parameter can only be VPC. Use the default setting.|
    |VPC VSwitch

|The virtual private cloud \(VPC\) and VSwitch of the new cluster. Select a VPC and a VSwitch from the drop-down lists, or [create a VPC and a VSwitch](https://vpc.console.aliyun.com). **Note:** Make sure that the PolarDB cluster to be created and the ECS instance to be connected are deployed in the same VPC. Otherwise, the cluster and the ECS instance cannot communicate over the VPC. This compromises performance. |
    |Compatibility|By default, the compatibility of the new cluster is consistent with that of the source cluster. For example, if the value of the Compatibility parameter is **MySQL 8.0** for the source cluster, the value of the Compatibility parameter is also **MySQL 8.0** for the new cluster. Use the default setting.|
    |Node Specification|The node specification of the new cluster. Select a specification based on your business needs. The maximum storage capacity and the performance of clusters vary based on the node specifications. For more information, see [Specifications and pricing](/intl.en-US/Pricing/Specifications and pricing.md).|
    |Nodes|The number of nodes in the new cluster. Use the default setting. The system automatically creates a read-only node that has the same specification as the primary node.|
    |Storage Cost|You do not need to specify this parameter. You are charged for the used storage space on an hourly basis. For more information, see [Specifications and pricing](/intl.en-US/Pricing/Specifications and pricing.md). **Note:** You do not need to select a storage capacity when you create a cluster. The system automatically scales the storage capacity based on the amount of data to be stored. |
    |Cluster Name|    -   The name of the new cluster. The cluster name must be 2 to 128 characters in length, and can contain digits, periods \(.\), underscores \(\_\), and hyphens \(-\).
    -   If you leave this parameter blank, the system automatically generates a cluster name. You can change the cluster name after the cluster is created. |
    |Purchase Plan|The subscription duration of the new cluster. This parameter is valid for only the source cluster whose **Billing Method** is **Subscription**.|
    |Number|The number of clusters. The value ranges from 1 to 50. The default value is 1.|

5.  Select the check box after you read the terms of the service agreement, and then click **Buy Now**.

    **Note:** After you complete the payment, wait 1 to 5 minutes until the cluster is created. Then, you can view the new cluster on the Clusters page.


