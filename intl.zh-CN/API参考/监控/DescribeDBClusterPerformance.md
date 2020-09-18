# DescribeDBClusterPerformance

调用DescribeDBClusterPerformance接口查询PolarDB集群的性能数据。

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

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=polardb&api=DescribeDBClusterPerformance&type=RPC&version=2017-08-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeDBClusterPerformance|系统规定参数，取值：**DescribeDBClusterPerformance**。 |
|DBClusterId|String|是|pc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|集群ID。 |
|EndTime|String|是|2012-06-08T15:00Z|查询结束时间。格式为`yyyy-MM-ddTHH:mmZ`（UTC时间）。 |
|Key|String|是|PolarDBDiskUsage|查询的性能指标，多个值间用英文逗号（,）分隔，详细参数请参见[性能参数表](~~141787~~)。

 **说明：** 最多可传入5个查询的性能指标。 |
|StartTime|String|是|2012-06-08T01:00Z|查询开始时间。格式为`yyyy-MM-ddTHH:mmZ`（UTC时间）。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DBClusterId|String|pc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|数据库集群ID。 |
|DBType|String|MySQL|兼容数据库类型。 |
|DBVersion|String|5.6|兼容数据库版本。 |
|EndTime|String|2012-06-08T15:00Z|查询结束时间。格式：`yyyy-MM-ddTHH:mmZ`（UTC时间）。 |
|PerformanceKeys|Array of PerformanceItem| |集群性能数据列表。 |
|PerformanceItem| | | |
|DBNodeId|String|pi-\*\*\*\*\*\*\*\*\*\*\*\*\*|数据库集群节点ID。

 **说明：** 当`Key`中的值设置为`PolarDBDiskUsage`时，不会返回该参数。 |
|Measurement|String|PolarDBDiskUsage|性能指标。 |
|MetricName|String|mean\_data\_size|具体的性能指标度量名称。 |
|Points|Array of PerformanceItemValue| |性能数据数组。 |
|PerformanceItemValue| | | |
|Timestamp|Long|1571193960000|监控指标的具体时间点，时间戳（毫秒ms）。 |
|Value|String|14.25|监控指标数据值。 |
|RequestId|String|A5409D02-D661-4BF3-8F3D-0A814D\*\*\*\*\*\*|请求ID。 |
|StartTime|String|2012-06-08T01:00Z|查询开始时间。格式：`yyyy-MM-ddTHH:mmZ`（UTC时间）。 |

## 示例

请求示例

```
http(s)://polardb.aliyuncs.com/?Action=DescribeDBClusterPerformance
&DBClusterId=pc-****************
&EndTime=2012-06-08T15:00Z
&Key=PolarDBDiskUsage
&StartTime=2012-06-08T01:00Z
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<code>200</code>
<data>
    <PerformanceKeys>
        <PerformanceItem>
            <Measurement>PolarDBDiskUsage</Measurement>
            <MetricName>mean_data_size</MetricName>
            <Points>
                <PerformanceItemValue>
                    <Timestamp>1571193960000</Timestamp>
                    <Value>14.25</Value>
                </PerformanceItemValue>
            </Points>
        </PerformanceItem>
    </PerformanceKeys>
    <DBVersion>5.6</DBVersion>
    <RequestId>A0ADCEAF-3277-48DE-B66D-4B67B1******</RequestId>
    <EndTime>2012-06-08T15:00Z</EndTime>
    <StartTime>2012-06-08T01:00Z</StartTime>
    <DBClusterId>pc-****************</DBClusterId>
    <DBType>MySQL</DBType>
</data>
<requestId>A0ADCEAF-3277-48DE-B66D-4B67B1******</requestId>
<successResponse>true</successResponse>
```

`JSON` 格式

```
{
    "code":"200",
    "data":{
        "PerformanceKeys":{
            "PerformanceItem":[
                {
                    "Measurement":"PolarDBDiskUsage",
                    "MetricName":"mean_data_size",
                    "Points": {
                        "PerformanceItemValue": [
                            {
                                "Timestamp": 1571193960000,
                                "Value": "14.25"
                            }
                        ]
                    }
                }
            ]
        },
        "DBVersion":"5.6",
        "RequestId":"A0ADCEAF-3277-48DE-B66D-4B67B1******",
        "EndTime":"2012-06-08T15:00Z",
        "StartTime":"2012-06-08T01:00Z",
        "DBClusterId":"pc-****************",
        "DBType":"MySQL"
    },
    "requestId":"A0ADCEAF-3277-48DE-B66D-4B67B1******",
    "successResponse":true
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/polardb)查看更多错误码。

