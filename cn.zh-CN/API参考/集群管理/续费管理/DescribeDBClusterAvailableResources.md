# DescribeDBClusterAvailableResources

调用DescribeDBClusterAvailableResources接口查询PolarDB集群可售卖资源。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=polardb&api=DescribeDBClusterAvailableResources&type=RPC&version=2017-08-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeDBClusterAvailableResources|系统规定参数，取值：**DescribeDBClusterAvailableResources**。 |
|PayType|String|是|Postpaid|付费类型，取值范围如下：

 -   **Postpaid**：按量付费（也称后付费或按小时付费）。
-   **Prepaid**：包年包月（也称预付费）。 |
|DBType|String|否|MySQL|数据库引擎类型，取值范围如下：

 -   **MySQL**
-   **PostgreSQL**
-   **Oracle** |
|DBVersion|String|否|5.6|数据库引擎版本号。

 -   MySQL版本号取值范围如下：
    -   **5.6**
    -   **5.7**
    -   **8.0**
-   PostgreSQL版本号取值为**11**。
-   Oracle版本号取值为**11**。 |
|DBNodeClass|String|否|polar.mysql.x4.large|节点规格，详情请参见[规格与定价](~~68498~~)。 |
|RegionId|String|否|cn-hangzhou|地域ID。默认为**cn-hangzhou**。

 **说明：** 可通过接口[DescribeRegions](~~98041~~)查看可用的地域。 |
|ZoneId|String|否|cn-hangzhou-i|可用区ID。

 **说明：** 可通过[DescribeRegions](~~98041~~)查看可用的可用区。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AvailableZones|Array of AvailableZone| |可售卖的资源信息列表。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|SupportedEngines|Array of SupportedEngine| |可售卖引擎列表。 |
|AvailableResources|Array of AvailableResource| |可售卖的资源列表。 |
|Category|String|Normal|集群系列，目前仅支持如下系列：

 -   **Normal**：标准版
-   **basic**：普惠版

**说明：** 普惠版目前仅支持PolarDB MySQL 5.6和8.0两个版本。 |
|DBNodeClass|String|polar.mysql.x4.large|节点规格。 |
|Engine|String|mysql57|数据库引擎版本。 |
|ZoneId|String|cn-hangzhou-i|可用区ID。 |
|RequestId|String|2B19F698-8FFC-4918-B9E2-58D878\*\*\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://polardb.aliyuncs.com/?Action=DescribeDBClusterAvailableResources
&PayType=Postpaid
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RequestId>5D070B24-40C5-4077-B526-DC1A03******</RequestId>
<AvailableZones>
    <ZoneId>cn-hangzhou-h</ZoneId>
    <RegionId>cn-hangzhou</RegionId>
    <SupportedEngines>
        <AvailableResources>
            <Category>Normal</Category>
            <DBNodeClass>polar.mysql.x4.large</DBNodeClass>
        </AvailableResources>
        <Engine>mysql57</Engine>
    </SupportedEngines>
</AvailableZones>
```

`JSON` 格式

```
{
	"RequestId": "2B19F698-8FFC-4918-B9E2-58D878******",
	"AvailableZones": [
		{
			"ZoneId": "cn-hangzhou-i",
			"RegionId": "cn-hangzhou",
			"SupportedEngines": [
				{
					"AvailableResources": [
						{
							"Category": "Normal",
							"DBNodeClass": "polar.mysql.x4.large"
						},
						{
							"Category": "Normal",
							"DBNodeClass": "polar.mysql.x4.xlarge"
						},
						{
							"Category": "Normal",
							"DBNodeClass": "polar.mysql.x8.xlarge"
						},
						{
							"Category": "Normal",
							"DBNodeClass": "polar.mysql.x8.2xlarge"
						},
						{
							"Category": "Normal",
							"DBNodeClass": "polar.mysql.x8.4xlarge"
						},
						{
							"Category": "Normal",
							"DBNodeClass": "polar.mysql.x8.8xlarge"
						},
						{
							"Category": "Normal",
							"DBNodeClass": "polar.mysql.x8.12xlarge"
						},
						{
							"Category": "Normal",
							"DBNodeClass": "polar.mysql.x4.medium"
						},
						{
							"Category": "basic",
							"DBNodeClass": "polar.mysql.s2.large"
						}
					],
					"Engine": "MySQL8.0"
				}
			]
		}
	]
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/polardb)查看更多错误码。

