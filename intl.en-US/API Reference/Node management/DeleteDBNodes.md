# DeleteDBNodes {#reference_187257 .reference}

You can call this operation to delete a node from a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_in0_nc4_4b7 .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DeleteDBNodes.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster whose node is to be deleted.|
|DBNodeId.N|String|Yes|The ID of the cluster node to be deleted. N is an integer that starts from 1. The maximum value of N is the number of current nodes minus 2. That is, each cluster must contain at least a primary node and a read-only node. **Note:** Currently, you can delete only a node at a time.

 |
|ClientToken|string|No|The client token that is used to ensure the idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The token is case-sensitive. It can contain only ASCII characters, and cannot exceed 64 characters in length.|

## Response parameters {#section_tqw_ftw_di4 .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|
|DBClusterId|String|The ID of the ApsaraDB for POLARDB cluster.|
|OrderId|String|The PO No. of the request.|

## Sample request {#section_avs_eu2_bkk .section}

```
https://polardb.aliyuncs.com/?Action=DeleteDBNodes
&DBClusterId=pc-xxxxxxxxxx
&DBNodeId.N=pi-xxxxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_hi6_s6e_bet .section}

XML format

```
<DeleteDBNodesResponse>  
	<RequestId>6566B2E6-3157-4B57-A693-AFB751E67C25</RequestId>
	<OrderId>2035638xxxxxxx</OrderId>
	<DBClusterId>pc-xxxxxxxxxx</DBClusterId>
</DeleteDBNodesResponse>
```

JSON format

```
{
	"RequestId": "6566B2E6-3157-4B57-A693-AFB751E67C25",
	"OrderId": 2035638xxxxxxx,
	"DBClusterId": "pc-xxxxxxxxxx"
}
```

