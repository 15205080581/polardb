# DescribeAutoRenewAttribute {#reference_221022 .reference}

You can call this operation to query the auto renewal attribute of subscription ApsaraDB for POLARDB clusters.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeAutoRenewAttribute.|
|RegionId|String|Yes|The ID of the region, which can be up to 50 characters in length. You can call the [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) operation to query available regions.|
|DBClusterIds|String|No|The ID of the ApsaraDB for POLARDB cluster to be queried. Separate multiple cluster IDs with a comma \(,\).|
|PageSize|String|No|The number of entries to return on each page. Valid values: -   30
-   50
-   100

 Default value: 30.|
|PageNumber|String|No|The number of the page to return. Valid values: any non-zero positive integer. Default value: 1.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|
|PageNumber|Integer|The number of the page returned.|
|TotalRecordCount|Integer|The total number of entries returned.|
|PageRecordCount|Integer|The total number of pages returned.|
|Items|List<AutoRenewAttribute\>|The list of the renewal information of clusters.|

## AutoRenewAttribute {#section_ilc_b3s_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|DBClusterId|String|The ID of the ApsaraDB for POLARDB cluster.|
|RegionId|String|The ID of the region.|
|AutoRenewEnabled|Boolean|Indicates whether auto renewal is enabled. Valid values: -   true: enabled
-   false: disabled

 |
|Duration|Integer|The renewal period of the subscription cluster.|
|PeriodUnit|String|The unit of the renewal period. Valid values: -   Year
-   Month

 |
|RenewalStatus|String|The renewal status of the cluster. Valid values: -   AutoRenewal: The cluster is automatically renewed.
-   Normal: The cluster is manually renewed. The system sends an SMS message to remind you before the cluster expires.
-   NotRenewal: The cluster is not renewed. The system does not send a reminder for expiration, but only sends an SMS message three days before the cluster expires to remind you that the cluster is not renewed.

 |

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeAutoRenewAttribute
&RegionId=cn-hangzhou
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<DescribeAutoRenewAttributeResponse>  
	<Items>
		<AutoRenewAttribute>
			<RenewalStatus>Normal</RenewalStatus>
			<Duration>1</Duration>
			<RegionId>cn-hangzhou</RegionId>
			<AutoRenewEnabled>true</AutoRenewEnabled>
			<PeriodUnit>Month</PeriodUnit>
			<DBClusterId>pc-xxxxxxxxxxxxxxxx</DBClusterId>
		</AutoRenewAttribute>
	</Items>
	<TotalRecordCount>1</TotalRecordCount>
	<PageNumber>1</PageNumber>
	<RequestId>8ABD1FF2-85B1-4D03-8C99-FB603B8AF82D</RequestId>
	<PageRecordCount>1</PageRecordCount>
</DescribeAutoRenewAttributeResponse>
```

JSON format

```
{
	"Items": {
		"AutoRenewAttribute": [
			{
				"RenewalStatus": "AutoRenewal",
				"Duration": 1,
				"RegionId": "cn-hangzhou",
				"AutoRenewEnabled": true,
				"PeriodUnit": "Month",
				"DBClusterId": "pc-xxxxxxxxxxxxxxxx"
			}
		]
	},
	"TotalRecordCount": 1,
	"PageNumber": 1,
	"RequestId": "8ABD1FF2-85B1-4D03-8C99-FB603B8AF82D",
	"PageRecordCount": 1
}
```

