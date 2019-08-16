# Set or release a custom cluster connection point {#concept_186667 .concept}

The system automatically generates a default connection point for a cluster. You can also manually add custom cluster connection points.

You can use custom connection points on a POLARDB for MySQL cluster. You can also set their read/write mode and consistency level and select associated read-only nodes based on different business scenarios. This enhances business flexibility.

**Note:** 

-   A cluster can have a maximum of four cluster connection points, including one default connection point and three custom connection points.
-   The default cluster connection point cannot be released. A custom cluster connection point can be released.
-   Like a custom cluster connection point, the default cluster connection point supports custom settings. For more information, see [Modify a custom cluster connection point](#section_6qz_cik_z5a).

## Prerequisites {#section_v7s_kbp_g0r .section}

You can directly add custom connection points for clusters created on and after April 29, 2019. For clusters created before April 29, 2019, you must [open a ticket](https://workorder.console.aliyun.com/console.htm#/ticket/add?productCode=polardb) before you can add custom cluster connection points.

## Add a custom cluster connection point {#section_vns_r12_bul .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Find the target cluster and click the cluster ID in the **Cluster Name** column.
4.  In the Access Information section on the Basics page, click **Create Custom Connection Point** next to **Cluster Connection Points \(Recommended\)**.

    ![Add a custom cluster connection point](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/160647/156594091145027_en-US.png)

5.  In the dialog box that appears, set parameters for creating a custom cluster connection point. The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Read/write Mode**|Select the read/write mode of the connection point. Valid values: **Read Only** and **Read and Write \(Automatic Read-write Splitting\)**. **Note:** You can also modify the read/write mode of a custom connection point after it is created. The modification takes effect only for the newly created connections. The existing connections remain in the original read/write mode.

 |
    |**Reader Nodes**|From the Unselected Nodes list on the left, select the nodes that you want to add to the connection point to process read requests. The available nodes include the primary node and all read-only nodes. The connection point only sends read requests to the selected nodes. **Note:** 

    -   Select at least two nodes.
    -   Write requests are sent only to the primary node regardless of whether the primary node is selected.
 |
    |**Automatically Add New Nodes**|Specify whether a newly added node will be automatically added to the connection point.|
    |**Load Balancing Policy**|The scheduling policy for read requests among multiple read-only nodes when read-write splitting is enabled. The value is fixed.|
    |**Consistency Level**|     -   **Eventual Consistency**: provides the best performance.
    -   **Session Consistency**: guarantees the read consistency at the session level. In this mode, the load of the primary node is slightly increased.
 For more information, see [../../../../dita-oss-bucket/SP\_61/DNPOLA1875676/EN-US\_TP\_76678\_V1.md\#](../../../../intl.en-US/.md#). **Note:** If the read/write mode is set to Read Only, the value is fixed to **Eventual Consistency**.

 |

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/160647/156594091145041_en-US.png)

6.  Click **OK**.

## Modify a custom cluster connection point {#section_6qz_cik_z5a .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Find the target cluster and click the cluster ID in the **Cluster Name** column.
4.  In the Access Information section on the Basics page, click **Modify** next to a **custom connection point**.

    ![Modify a custom cluster connection point](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/160647/156594091147219_en-US.png)

5.  In the dialog box that appears, set parameters for modifying a custom cluster connection point. The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Read/write Mode**|Select the read/write mode of the connection point. Valid values: **Read Only** and **Read and Write \(Automatic Read-write Splitting\)**.|
    |**Reader Nodes**|From the Unselected Nodes list on the left, select the nodes that you want to add to the connection point to process read requests. The available nodes include the primary node and all read-only nodes. The connection point only sends read requests to the selected nodes. **Note:** 

    -   Select at least two nodes.
    -   Write requests are sent only to the primary node regardless of whether the primary node is selected.
    -   Adding nodes to a connection point does not affect the use of the connection point. However, when a node is removed from the connection point, the persistent connection on the node is interrupted.
 |
    |**Automatically Add New Nodes**|Specify whether a newly added node will be automatically added to the connection point.|
    |**Load Balancing Policy**|The scheduling policy for read requests among multiple read-only nodes when read-write splitting is enabled. The value is fixed.|
    |**Consistency Level**|     -   **Eventual Consistency**: provides the best performance.
    -   **Session Consistency**: guarantees the read consistency at the session level. In this mode, the load of the primary node is slightly increased.
 For more information, see [../../../../dita-oss-bucket/SP\_61/DNPOLA1875676/EN-US\_TP\_76678\_V1.md\#](../../../../intl.en-US/.md#). **Note:** 

    -   If the read/write mode is set to Read Only, the value is fixed to **Eventual Consistency**.
    -   The modification of the consistency level immediately takes effect for all connections.
 |

6.  Click **OK**.

## Release a custom cluster connection point {#section_mp8_yam_nfz .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Find the target cluster and click the cluster ID in the **Cluster Name** column.
4.  In the Access Information section on the Basics page, find the target custom connection point under **Cluster Connection Points \(Recommended\)**, and click **Delete**.

    ![Release a custom cluster connection point](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/160647/156594091245049_en-US.png)

5.  In the dialog box that appears, click **OK**.

## Related API operations {#section_k9l_gm9_cpu .section}

|API operation|Description|
|-------------|-----------|
|[CreateDBClusterEndpoint](../../../../intl.en-US/API Reference/Connection points/CreateDBClusterEndpoint.md#)|Creates a custom cluster connection point.|
|[DescribeDBClusterEndpoints](../../../../intl.en-US/API Reference/Connection points/DescribeDBClusterEndpoints.md#)|Queries cluster connection points.|
|[ModifyDBClusterEndpoint](../../../../intl.en-US/API Reference/Connection points/ModifyDBClusterEndpoint.md#)|Modifies a cluster connection point.|
|[DeleteDBClusterEndpoint](../../../../intl.en-US/API Reference/Connection points/DeleteDBClusterEndpoint.md#)|Releases a custom cluster connection point.|

