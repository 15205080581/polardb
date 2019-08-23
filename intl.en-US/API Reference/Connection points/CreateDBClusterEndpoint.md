# CreateDBClusterEndpoint {#reference_ghp_s25_xfb .reference}

You can call this operation to create a custom connection point for a specified ApsaraDB for POLARDB cluster.

**Note:** Currently, POLARDB for PostgreSQL and POLARDB for Oracle do not support custom connection points.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to CreateDBClusterEndpoint.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster for which a custom connection point is to be created.|
|EndpointType|String|Yes|The type of the cluster connection point. Set this parameter to Custom.|
|ReadWriteMode|String|No|The read/write mode of the cluster connection point. Valid values: -   ReadWrite: receives and forwards read and write requests \(automatic read-write splitting\).
-   ReadOnly: receives and forwards only read requests.

 Default value: ReadOnly.|
|Nodes|String|No|The nodes to be added to this connection point to process read requests from this connection point. Add at least two nodes and separate them with a comma \(,\). If you do not specify this parameter, all nodes of the cluster are added to this connection point by default.

 |
|AutoAddNewNodes|String|No|Specifies whether a newly added node is automatically added to this connection point. Valid values: -   Enable
-   Disable

 Default value: Disable.

 |
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

```
https://polardb.aliyuncs.com/?Action=CreateDBClusterEndpoint
&DBClusterId=pc-xxxxxxxxxxxxxxxxxx
&EndpointType=Custom
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<CreateDBClusterEndpointResponse>  
    <RequestId>CD35F3-F3-44CA-AFFF-BAF869666D6B</RequestId>
</CreateDBClusterEndpointResponse>
```

JSON format

```
{
    "RequestId": "CD35F3-F3-44CA-AFFF-BAF869666D6B"
}
```

