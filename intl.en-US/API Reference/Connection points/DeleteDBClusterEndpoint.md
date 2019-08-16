# DeleteDBClusterEndpoint {#reference_189542 .reference}

You can call this operation to release a custom connection point for a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DeleteDBClusterEndpoint.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to which a custom connection point belongs.|
|EndpointId|String|Yes|The ID of the custom connection point to be released. For example, pe-xxxxxxxx.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_lx1_c25_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DeleteDBClusterEndpoint
&DBClusterId=pc-xxxxxxxxxxxxxxxxxx
&EndpointId=pe-xxxxxxxxxxxxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<DeleteDBClusterEndpointResponse>  
	<RequestId>CD3FA5F3-FAF3-44CA-AFFF-BAF869666D6B</RequestId>
</DeleteDBClusterEndpointResponse>
```

JSON format

```
{
	"RequestId": "CD3FA5F3-FAF3-44CA-AFFF-BAF869666D6B"
}
```

