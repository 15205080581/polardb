# RestartDBNode {#reference_zpr_h5t_xfb .reference}

You can call this operation to restart a specified node of an ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to RestartDBNode.|
|DBNodeId|String|Yes|The ID of the cluster node to be restarted.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_khc_1dz_xfb .section}

```
https://polardb.aliyuncs.com/?Action=RestartDBNode
&DBClusterId=pc-xxxxxxxxxx
&DBNodeId=pi-xxxxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<RestartDBNodeResponse>  
	<RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</RestartDBNodeResponse>
```

JSON format

```
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

