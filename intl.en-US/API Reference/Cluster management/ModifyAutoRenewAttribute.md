# ModifyAutoRenewAttribute {#reference_220995 .reference}

You can call this operation to set the auto renewal attribute for a specified subscription ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyAutoRenewAttribute.|
|DBClusterIds|String|Yes|The ID of the ApsaraDB for POLARDB cluster whose auto renewal attribute is to be set.|
|RegionId|String|Yes|The ID of the region, which can be up to 50 characters in length. You can call the [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) operation to query available regions.|
|RenewalStatus|String|No|The auto renewal status of the cluster. Valid values: -   AutoRenewal: automatically renews the cluster.
-   Normal: manually renews the cluster.
-   NotRenewal: does not renew the cluster.

 Default value: AutoRenewal.

 **Note:** If this parameter is set to NotRenewal, the system does not send a reminder for expiration, but only sends an SMS message three days before the cluster expires to remind you that the cluster is not renewed.

 |
|PeriodUnit|String|No|The unit of the renewal period. Valid values: -   Year
-   Month

 Default value: Month.

 |
|Duration|String|No|The auto renewal period of the subscription cluster. The valid values depend on the value specified in the PeriodUnit parameter. Valid values: -   Month: 1, 2, 3, 6, and 12
-   Year: \[1, 3\]

 Default value: 1.

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ModifyAutoRenewAttribute
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&RegionId=cn-hangzhou
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<ModifyAutoRenewAttributeResponse>  
	<RequestId>4CE6DF97-AEA4-484F-906F-C407EE3770EB</RequestId>
</ModifyAutoRenewAttributeResponse>
```

JSON format

```
{
	"RequestId": "4CE6DF97-AEA4-484F-906F-C407EE3770EB"
}
```

