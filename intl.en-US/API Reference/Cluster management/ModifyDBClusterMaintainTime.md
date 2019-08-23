# ModifyDBClusterMaintainTime {#reference_bkt_kjs_xfb .reference}

You can call this operation to modify the maintenance window of a specified ApsaraDB for POLARDB cluster. You can select a period of time during off-peak hours. Alibaba Cloud maintains your clusters within the specified maintenance window to minimize the impact on your business.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyDBClusterMaintainTime.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster whose maintenance window is to be modified.|
|MaintainTime|String|Yes|The maintenance window of the cluster. Specify the time in the *HH:mm*Z- *HH:mm*Z format.

 For example, a value of 16:00Z-17:00Z indicates that the cluster can be maintained from 00:00 to 01:00 \(UTC+8\).

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ModifyDBClusterMaintainTime
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&MaintainTime=02:00Z-03:00Z
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<ModifyDBClusterMaintainTimeResponse>  
	<RequestId>70656639-1416-479F-AF13-D08197F9C43B</RequestId>
</ModifyDBClusterMaintainTimeResponse>
```

JSON format

```
{
    "RequestId":"70656639-1416-479F-AF13-D08197F9C43B"
}
```

