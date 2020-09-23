# DescribeDBClusterPerformance

Queries the performance data of a PolarDB cluster.

-   The monitoring data is collected once every 5 seconds:
    -   If the query time range is less than or equal to 1 hour, the data is displayed at intervals of 5 seconds.
    -   If the query time range is less than or equal to one day, the data is displayed at intervals of 1 minute.
    -   If the query time range is less than or equal to seven days, the data is displayed at intervals of 10 minutes.
    -   If the query time range is less than or equal to 30 days, the data is displayed at intervals of 1 hour.
    -   If the query time range is greater than 30 days, the data is displayed at intervals of one day.
-   The monitoring data is collected once every 60 seconds:
    -   If the query time range is less than or equal to one day, the data is displayed at intervals of 1 minute.
    -   If the query time range is less than or equal to seven days, the data is displayed at intervals of 10 minutes.
    -   If the query time range is less than or equal to 30 days, the data is displayed at intervals of 1 hour.
    -   If the query time range is greater than 30 days, the data is displayed at intervals of one day.

**Note:** By default, the monitoring data is collected once every 60 seconds. You can call the [ModifyDBClusterMonitor](~~159557~~) operation to set the data collection interval to every 5 seconds.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=polardb&api=DescribeDBClusterPerformance&type=RPC&version=2017-08-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|DescribeDBClusterPerformance|The operation that you want to perform. Set the value to **DescribeDBClusterPerformance**. |
|DBClusterId|String|Yes|pc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|The ID of the PolarDB cluster. |
|EndTime|String|Yes|2012-06-08T15:00Z|The end of the time range to query. Specify the time in the `yyyy-MM-ddTHH:mmZ` format. The time must be in UTC. |
|Key|String|Yes|PolarDBDiskUsage|The performance indicators that you want to query. Separate multiple indicators with commas \(,\). For more information, see [Performance parameters](~~141787~~).

 **Note:** You can specify a maximum of five performance indicators. |
|StartTime|String|Yes|2012-06-08T01:00Z|The beginning of the time range to query. Specify the time in the `yyyy-MM-ddTHH:mmZ` format. The time must be in UTC. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBClusterId|String|pc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|The ID of the PolarDB cluster. |
|DBType|String|MySQL|The engine of the database. |
|DBVersion|String|5.6|The version of the database engine. |
|EndTime|String|2012-06-08T15:00Z|The end of the time range. The time is in the `yyyy-MM-ddTHH:mmZ` format. The time is displayed in UTC. |
|PerformanceKeys|Array of PerformanceItem| |The list of cluster performance indicators. |
|PerformanceItem| | | |
|DBNodeId|String|pi-\*\*\*\*\*\*\*\*\*\*\*\*\*|The ID of the cluster node.

 **Note:** The value of this parameter is not returned if `Key` is set to `PolarDBDiskUsage`. |
|Measurement|String|PolarDBDiskUsage|The performance indicator. |
|MetricName|String|mean\_data\_size|The name of the metric. |
|Points|Array of PerformanceItemValue| |The array of the metrics. |
|PerformanceItemValue| | | |
|Timestamp|Long|1571193960000|The timestamp of the metric. Unit: milliseconds. |
|Value|String|14.25|The value of the metric. |
|RequestId|String|A5409D02-D661-4BF3-8F3D-0A814D\*\*\*\*\*\*|The ID of the request. |
|StartTime|String|2012-06-08T01:00Z|The beginning of the time range. The time is in the `yyyy-MM-ddTHH:mmZ` format. The time is displayed in UTC. |

## Examples

Sample requests

```
http(s)://polardb.aliyuncs.com/? Action=DescribeDBClusterPerformance
&DBClusterId=pc-****************
&EndTime=2012-06-08T15:00Z
&Key=PolarDBDiskUsage
&StartTime=2012-06-08T01:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/polardb).

