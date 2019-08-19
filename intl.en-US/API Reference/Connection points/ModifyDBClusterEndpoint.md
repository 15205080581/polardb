# ModifyDBClusterEndpoint {#reference_189417 .reference}

You can call this operation to modify the connection point attributes of a specified ApsaraDB for POLARDB cluster.

**Note:** Currently, POLARDB for PostgreSQL and POLARDB for Oracle do not support cluster connection points.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyDBClusterEndpoint.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to which a cluster connection point belongs.|
|EndpointId|String|Yes|The ID of the cluster connection point whose attributes are to be modified. For example, pe-xxxxxxxx.|
|ReadWriteMode|String|No|The read/write mode of the cluster connection point. Valid values: -   ReadWrite: receives and forwards read and write requests \(automatic read-write splitting\).
-   ReadOnly: receives and forwards only read requests.

 Default value: ReadOnly.|
|Nodes|String|No|The nodes to be added to this connection point to process read requests from this connection point. Add at least two nodes and separate them with a comma \(,\). If you do not specify this parameter, all nodes of the cluster are added to this connection point by default.

 |
|AutoAddNewNodes|String|No|Specifies whether a newly added node is automatically added to this connection point. Valid values: -   Enable
-   Disable

 Default value: Disable.|
|EndpointConfig|String|No|The consistency level of the cluster connection point. Specify this parameter in the `{"ConsistLevel": "<level>"}` format. Valid values: -   0: eventual consistency
-   1: session consistency

 For example, `{"ConsistLevel": "0"}`.

 **Note:** If the ReadWriteMode parameter is set to ReadOnly, the value of this parameter must be 0.

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_lx1_c25_xfb .section}

``` {#codeblock_s0k_5hy_eil}
https://polardb.aliyuncs.com/?Action=ModifyDBClusterEndpoint
&DBClusterId=pc-xxxxxxxxxxxxxxxxxx
&EndpointId=pe-xxxxxxxxxxxxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_unp_ypy_pfz}
<ModifyDBClusterEndpointResponse>  
    <RequestId>CD3FA5F3-FAF3-44CA-AFFF-BAF869666D6B</RequestId>
</ModifyDBClusterEndpointResponse>
```

JSON format

``` {#codeblock_y4x_c7s_u0f}
{
    "RequestId": "CD3FA5F3-FAF3-44CA-AFFF-BAF869666D6B"
}
```

