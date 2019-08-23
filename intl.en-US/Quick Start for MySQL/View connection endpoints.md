# View connection endpoints {#concept_imd_wlq_tdb .concept}

A POLARDB cluster includes cluster connection endpoints and primary endpoints.

## Procedure {#section_rc4_ceb_45t .section}

1.  Log on to the [POLARDB console](https://polardb.console.aliyun.com).
2.  Find the target POLARDB cluster and click its ID.
3.  In the **Access Information** on the Basics page, view the connection endpoints of the POLARDB cluster.

## Cluster and primary connection endpoints {#section_47j_7wk_us8 .section}

|Type|Description|Supported network type|Procedure|
|----|-----------|----------------------|---------|
|Cluster connection endpoint \(recommended\)|An application only needs to connect to a cluster connection endpoint, then it can connect to all the nodes in the POLARDB cluster. The cluster endpoint supports read/write splitting. It sends write requests to the primary node and read requests to the primary and read-only nodes and can automatically balance load among these nodes. **Note:** The POLARDB cluster contains one default cluster connection endpoint. You can customize one or more cluster connection endpoints as needed. A custom connection endpoint can connect to specified nodes and work in the specified read/write mode. For more information, see [Set or release a custom cluster connection point](../../../../intl.en-US/User Guide for MySQL/Connect to POLARDB/Set or release a custom cluster connection endpoint.md#).

 |VPC and public network| 1.  Find the target POLARDB cluster and click its ID.
2.  In the **Access Information** on the Basics page, view the connection endpoints of the POLARDB cluster.

 |
|Primary connection endpoint|A primary connection endpoint always connects to the primary node and supports read and write operations. If the primary node becomes faulty, the primary endpoint is automatically switched to the read-only node that is promoted to the primary node.|VPC and public network|

![连接地址示意图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3018/156652761145542_en-US.png)

## Private and public connection endpoints {#section_3n5_mt5_rnu .section}

|Type|Description|Application scenario|
|----|-----------|--------------------|
|Private connection endpoint| -   Accessing the POLARDB cluster through a private connection endpoint maximizes performance.
-   A private connection endpoint cannot be released.

 | For example:

 -   If your ECS instance is located in the same VPC as the POLARDB cluster, then your ECS instance can communicate with the POLARDB cluster through the VPC.
-   You can access the POLARDB cluster through a VPC by using DMS.

 |
|Public connection endpoint| -   You must manually apply for a public connection endpoint, which can be released.
-   The public network refers to the Internet. Accessing the POLARDB cluster through the Internet cannot maximize performance.

 |For example, you can access the POLARDB cluster through the Internet to perform maintenance.|

## APIs {#section_nok_abg_88w .section}

|API|Description|
|:--|:----------|
|[DescribeDBClusterEndpoints](../../../../intl.en-US/API Reference/Connection points/DescribeDBClusterEndpoints.md#)|Used to the connection endpoints of a POLARDB cluster.|
|[CreateDBEndpointAddress](../../../../intl.en-US/API Reference/Connection points/CreateDBEndpointAddress.md#)|Used to create a public connection endpoint for a POLARDB cluster.|
|[ModifyDBEndpointAddress](../../../../intl.en-US/API Reference/Connection points/ModifyDBEndpointAddress.md#)|Used to change the default connection endpoint of a POLARDB cluster.|
|[DeleteDBEndpointAddress](../../../../intl.en-US/API Reference/Connection points/DeleteDBEndpointAddress.md#)|Used to release a cluster connection endpoint for a POLARDB cluster.|

## Network Type {#section_xxt_kpv_tdb .section}

|Network Type|Description|Application Scenario|
|------------|-----------|--------------------|
|VPC| -   This is a default connection endpoint in the VPC. You cannot release this connection endpoint.
-   POLARDB can achieve optimal performance when accessed in the VPC.

 | For example:

 -   An ECS instance can access databases through VPC if they are in the same VPC.
-   You can access POLARDB databases using DMS in the VPC.

 |
|Public network| -   You need to apply for a public network connection endpoint to access POLARDB databases, and can release such connection endpoints.
-   The public network is the Internet. POLARDB databases cannot achieve optimal performance if it is accessed through the public network.

 |You can access and maintain your POLARDB databases through the public network.|

