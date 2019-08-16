# ModifyDBNodeClass {#reference_187265 .reference}

You can call this operation to change the node specifications of a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_nwt_f3f_wvw .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyDBNodeClass.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster whose node specifications are to be changed.|
|ModifyType|String|No|The change type of the node specifications. Valid values: -   Upgrade: upgrades the node specifications.
-   Downgrade: downgrades the node specifications.

 |
|DBNodeTargetClass|String|No|The target node specifications of the cluster. For more information, see [../../../../dita-oss-bucket/SP\_61/DNPOLA1875676/EN-US\_TP\_3012.md\#](../../../../intl.en-US/Pricing/Specifications and pricing.md#).|
|ClientToken|String|No|The client token that is used to ensure the idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The token is case-sensitive. It can contain only ASCII characters, and cannot exceed 64 characters in length.|

## Response parameters {#section_i2b_pu2_yzg .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|
|DBClusterId|String|The ID of the ApsaraDB for POLARDB cluster.|
|OrderId|String|The PO No. of the request.|

## Sample request {#section_2zx_5jd_b5u .section}

```
https://polardb.aliyuncs.com/?Action=ModifyDBNodeClass
&DBClusterId=pc-xxxxxxxxxx
&ModifyType=Upgrade
&DBNodeTargetClass=polar.mysql.x4.large
&<[Common request parameters]>
```

## Sample response {#section_793_j2x_mn9 .section}

XML format

```
<ModifyDBNodeClassResponse>  
	<RequestId>685F028C-4FCD-407D-A559-072D6378C4C3</RequestId>
	<OrderId>2035629xxxxxx</OrderId>
	<DBClusterId>pc-xxxxxxxxxxxxx</DBClusterId>
</ModifyDBNodeClassResponse>
```

JSON format

```
{
	"RequestId": "685F028C-4FCD-407D-A559-072D6378C4C3",
	"OrderId": 2035629xxxxxx,
	"DBClusterId": "pc-xxxxxxxxxxxxx"
}
```

