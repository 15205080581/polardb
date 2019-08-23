# DescribeAutoRenewAttribute {#reference_221022 .reference}

该接口用于查询POLARDB包年包月集群自动续费状态。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeAutoRenewAttribute。|
|RegionId|String|是|地域ID，长度不超过50个字符，通过接口[DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#)查看可用的地域。|
|DBClusterIds|String|否|集群ID。多个集群用英文逗号“,”分隔。|
|PageSize|String|否|每页记录数，取值： -   30；
-   50；
-   100。

 默认值：30。|
|PageNumber|String|否|页码。取值为大于0且不超过Integer数据类型的的最大值，默认值为1。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|RequestId。|
|PageNumber|Integer|页数。|
|TotalRecordCount|Integer|总记录数。|
|PageRecordCount|Integer|总页数。|
|Items|List<AutoRenewAttribute\>|集群续费信息列表。|

## AutoRenewAttribute {#section_ilc_b3s_xfb .section}

|参数|类型|描述|
|:-|:-|:-|
|DBClusterId|String|集群ID。|
|RegionId|String|地域ID。|
|AutoRenewEnabled|Boolean|是否开启自动续费： -   true：开启；
-   false：关闭。

 |
|Duration|Integer|续费时长。|
|PeriodUnit|String|时长单位： -   Year：年；
-   Month：月。

 |
|RenewalStatus|String|续费状态，取值： -   AutoRenewal：自动续费；
-   Normal：手动续费，到期前短信提醒；
-   NotRenewal：到期不续费，到期前无提醒，只在到期前第三天发送不续费提醒。

 |

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeAutoRenewAttribute
&RegionId=cn-hangzhou
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

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

JSON格式

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

