# ModifyDBClusterDescription {#reference_k3t_pns_xfb .reference}

You can call this operation to modify the description of a specified ApsaraDB for POLARDB cluster to facilitate cluster maintenance.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyDBClusterDescription.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster whose description is to be modified.|
|DBClusterDescription|String|Yes|The description of the cluster. The description must comply with the following rules: -   It must start with a Chinese character or an English letter.
-   It can contain Chinese and English characters, digits, underscores \(\_\), and hyphens \(-\).
-   It cannot start with http:// or https://.
-   It must be 2 to 256 characters in length.

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ModifyDBClusterDescription
&DBClusterId=pc-xxxxxxxxxxxxxxxxx
&DBClusterDescription=ClusterDescriptionTest
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<ModifyDBClusterDescriptionResponse>  
	<RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</ModifyDBClusterDescriptionResponse>
```

JSON format

```
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

