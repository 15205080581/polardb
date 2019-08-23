# DeleteDBCluster {#reference_afp_n25_xfb .reference}

You can call this operation to delete a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DeleteDBCluster.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to be deleted.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_lx1_c25_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DeleteDBCluster
&DBClusterId=pc-xxxxxxxxxxxxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<DeleteDBClusterResponse>  
	<RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</DeleteDBClusterResponse>
```

JSON format

```
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

