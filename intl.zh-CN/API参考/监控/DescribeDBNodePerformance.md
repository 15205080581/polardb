# DescribeDBNodePerformance

调用DescribeDBNodePerformance查询PolarDB集群节点的性能数据。

-   若监控频率为5秒/次：
    -   当查询时间范围小于等于1小时，显示粒度为5秒。
    -   当查询时间范围小于等于1天，显示粒度为1分钟。
    -   当查询时间范围小于等于7天，显示粒度为10分钟。
    -   当查询时间范围小于等于30天，显示粒度为1小时。
    -   当查询范围大于30天，显示粒度为1天。
-   若监控频率为60秒/次：
    -   当查询范围小于等于1天，显示粒度为1分钟。
    -   当查询范围小于等于7天，显示粒度为10分钟。
    -   当查询范围小于等于30天，显示粒度为1小时。
    -   当查询范围大于30天，显示粒度为1天。

**说明：** 监控频率默认为60秒/次，您可以调用[ModifyDBClusterMonitor](~~159557~~)接口将其设置为5秒/次。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=polardb&api=DescribeDBNodePerformance&type=RPC&version=2017-08-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeDBNodePerformance|系统规定参数，取值为**DescribeDBNodePerformance**。 |
|DBNodeId|String|是|pi-\*\*\*\*\*\*\*\*\*\*\*\*\*|数据库集群节点ID。 |
|EndTime|String|是|2020-09-23T01:01Z|查询结束时间。格式为`yyyy-MM-ddTHH:mmZ`（UTC时间）。 |
|Key|String|是|PolarDBDiskUsage|查询的性能指标，多个值间用英文逗号（,）分隔，详细参数请参见[性能参数表](~~141787~~)。

 **说明：** 最多可传入5个查询的性能指标。 |
|StartTime|String|是|2020-09-23T01:00Z|查询开始时间。格式为`yyyy-MM-ddTHH:mmZ`（UTC时间）。 |
|DBClusterId|String|否|pc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|集群ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DBNodeId|String|pi-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|数据库集群节点ID。 |
|DBType|String|MySQL|兼容数据库类型。 |
|DBVersion|String|8.0|兼容数据库版本。 |
|EndTime|String|2020-09-23T01:01:00Z|查询结束时间。格式为`yyyy-MM-ddTHH:mm:ssZ`（UTC时间）。 |
|PerformanceKeys|Array of PerformanceItem| |集群性能数据列表。 |
|PerformanceItem| | | |
|Measurement|String|PolarDBDiskUsage|性能指标。 |
|MetricName|String|mean\_sys\_dir\_size|具体的性能指标度量名称。 |
|Points|Array of PerformanceItemValue| |性能数据数组。 |
|PerformanceItemValue| | | |
|Timestamp|Long|1600822800000|监控指标的具体时间点，格式为Unix时间戳，单位为毫秒（ms）。 |
|Value|String|9.33|监控指标数据值。 |
|RequestId|String|E2FDB684-751D-424D-98B9-704BEA\*\*\*\*\*\*|请求ID。 |
|StartTime|String|2020-09-23T01:00:00Z|查询开始时间。格式为`yyyy-MM-ddTHH:mm:ssZ`（UTC时间）。 |

## 示例

请求示例

```
http(s)://polardb.aliyuncs.com/?Action=DescribeDBNodePerformance
&DBNodeId=pi-*************
&EndTime=2020-09-23T01:01Z
&Key=PolarDBDiskUsage
&StartTime=2020-09-23T01:00Z
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<PerformanceKeys>
    <PerformanceItem>
        <Measurement>PolarDBDiskUsage</Measurement>
        <MetricName>mean_binlog_size</MetricName>
        <Points>
            <PerformanceItemValue>
                <Value>0.00</Value>
                <Timestamp>1600822800000</Timestamp>
            </PerformanceItemValue>
        </Points>
    </PerformanceItem>
    <PerformanceItem>
        <Measurement>PolarDBDiskUsage</Measurement>
        <MetricName>mean_data_size</MetricName>
        <Points>
            <PerformanceItemValue>
                <Value>42.38</Value>
                <Timestamp>1600822800000</Timestamp>
            </PerformanceItemValue>
        </Points>
    </PerformanceItem>
    <PerformanceItem>
        <Measurement>PolarDBDiskUsage</Measurement>
        <MetricName>mean_log_size</MetricName>
        <Points>
            <PerformanceItemValue>
                <Value>4393.63</Value>
                <Timestamp>1600822800000</Timestamp>
            </PerformanceItemValue>
        </Points>
    </PerformanceItem>
    <PerformanceItem>
        <Measurement>PolarDBDiskUsage</Measurement>
        <MetricName>mean_other_log_size</MetricName>
        <Points>
            <PerformanceItemValue>
                <Value>1.63</Value>
                <Timestamp>1600822800000</Timestamp>
            </PerformanceItemValue>
        </Points>
    </PerformanceItem>
    <PerformanceItem>
        <Measurement>PolarDBDiskUsage</Measurement>
        <MetricName>mean_redolog_size</MetricName>
        <Points>
            <PerformanceItemValue>
                <Value>4096.00</Value>
                <Timestamp>1600822800000</Timestamp>
            </PerformanceItemValue>
        </Points>
    </PerformanceItem>
    <PerformanceItem>
        <Measurement>PolarDBDiskUsage</Measurement>
        <MetricName>mean_sys_dir_size</MetricName>
        <Points>
            <PerformanceItemValue>
                <Value>9.33</Value>
                <Timestamp>1600822800000</Timestamp>
            </PerformanceItemValue>
        </Points>
    </PerformanceItem>
    <PerformanceItem>
        <Measurement>PolarDBDiskUsage</Measurement>
        <MetricName>mean_tmp_dir_size</MetricName>
        <Points>
            <PerformanceItemValue>
                <Value>0.00</Value>
                <Timestamp>1600822800000</Timestamp>
            </PerformanceItemValue>
        </Points>
    </PerformanceItem>
    <PerformanceItem>
        <Measurement>PolarDBDiskUsage</Measurement>
        <MetricName>mean_undolog_size</MetricName>
        <Points>
            <PerformanceItemValue>
                <Value>296.00</Value>
                <Timestamp>1600822800000</Timestamp>
            </PerformanceItemValue>
        </Points>
    </PerformanceItem>
</PerformanceKeys>
<DBVersion>8.0</DBVersion>
<RequestId>E2FDB684-751D-424D-98B9-704BEA******</RequestId>
<EndTime>2020-09-23T01:01:00Z</EndTime>
<StartTime>2020-09-23T01:00:00Z</StartTime>
<DBNodeId>pi-*****************</DBNodeId>
<DBType>MySQL</DBType>
```

`JSON` 格式

```
{
	"PerformanceKeys": {
		"PerformanceItem": [
			{
				"Measurement": "PolarDBDiskUsage",
				"MetricName": "mean_binlog_size",
				"Points": {
					"PerformanceItemValue": [
						{
							"Value": "0.00",
							"Timestamp": 1600822800000
						}
					]
				}
			},
			{
				"Measurement": "PolarDBDiskUsage",
				"MetricName": "mean_data_size",
				"Points": {
					"PerformanceItemValue": [
						{
							"Value": "42.38",
							"Timestamp": 1600822800000
						}
					]
				}
			},
			{
				"Measurement": "PolarDBDiskUsage",
				"MetricName": "mean_log_size",
				"Points": {
					"PerformanceItemValue": [
						{
							"Value": "4393.63",
							"Timestamp": 1600822800000
						}
					]
				}
			},
			{
				"Measurement": "PolarDBDiskUsage",
				"MetricName": "mean_other_log_size",
				"Points": {
					"PerformanceItemValue": [
						{
							"Value": "1.63",
							"Timestamp": 1600822800000
						}
					]
				}
			},
			{
				"Measurement": "PolarDBDiskUsage",
				"MetricName": "mean_redolog_size",
				"Points": {
					"PerformanceItemValue": [
						{
							"Value": "4096.00",
							"Timestamp": 1600822800000
						}
					]
				}
			},
			{
				"Measurement": "PolarDBDiskUsage",
				"MetricName": "mean_sys_dir_size",
				"Points": {
					"PerformanceItemValue": [
						{
							"Value": "9.33",
							"Timestamp": 1600822800000
						}
					]
				}
			},
			{
				"Measurement": "PolarDBDiskUsage",
				"MetricName": "mean_tmp_dir_size",
				"Points": {
					"PerformanceItemValue": [
						{
							"Value": "0.00",
							"Timestamp": 1600822800000
						}
					]
				}
			},
			{
				"Measurement": "PolarDBDiskUsage",
				"MetricName": "mean_undolog_size",
				"Points": {
					"PerformanceItemValue": [
						{
							"Value": "296.00",
							"Timestamp": 1600822800000
						}
					]
				}
			}
		]
	},
	"DBVersion": "8.0",
	"RequestId": "E2FDB684-751D-424D-98B9-704BEA******",
	"EndTime": "2020-09-23T01:01:00Z",
	"StartTime": "2020-09-23T01:00:00Z",
	"DBNodeId": "pi-*****************",
	"DBType": "MySQL"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/polardb)查看更多错误码。

