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
|EndTime|String|Yes|2020-09-23T01:00Z|The end of the time range to query. Specify the time in the `yyyy-MM-ddTHH:mmZ` format. The time must be in UTC. |
|Key|String|Yes|PolarDBDiskUsage|The performance indicators that you want to query. Separate multiple indicators with commas \(,\). For more information, see [Performance parameters](~~141787~~).

**Note:** You can specify a maximum of five performance indicators. |
|StartTime|String|Yes|2020-09-23T01:01Z|The beginning of the time range to query. Specify the time in the `yyyy-MM-ddTHH:mmZ` format. The time must be in UTC. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DBClusterId|String|pc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|The ID of the PolarDB cluster. |
|DBType|String|MySQL|The engine of the database. |
|DBVersion|String|8.0|The version of the database engine. |
|EndTime|String|2020-09-23T01:01:00Z|The end of the time range. The time is in the `yyyy-MM-ddTHH:mm:ssZ` format. The time is displayed in UTC. |
|PerformanceKeys|Array of PerformanceItem| |The list of cluster performance indicators. |
|PerformanceItem| | | |
|DBNodeId|String|pi-\*\*\*\*\*\*\*\*\*\*\*\*\*|The ID of the cluster node.

**Note:** The value of this parameter is not returned if `Key`is set to `PolarDBDiskUsage`. |
|Measurement|String|PolarDBDiskUsage|The performance indicator. |
|MetricName|String|mean\_data\_size|The name of the metric. |
|Points|Array of PerformanceItemValue| |The array of the metrics. |
|PerformanceItemValue| | | |
|Timestamp|Long|1600822800000|The timestamp of the metric. Unit: milliseconds. |
|Value|String|42.38|The value of the metric. |
|RequestId|String|35D3E3DA-4650-407A-BFF5-59BFF1\*\*\*\*\*\*|The ID of the request. |
|StartTime|String|2020-09-23T01:00:00Z|The beginning of the time range. The time is in the `yyyy-MM-ddTHH:mmZ` format. The time is displayed in UTC. |

## Examples

Sample requests

```
http(s)://polardb.aliyuncs.com/?Action=DescribeDBClusterPerformance
&DBClusterId=pc-****************
&EndTime=2020-09-23T01:00Z
&Key=PolarDBDiskUsage
&StartTime=2020-09-23T01:01Z
&<Common request parameters>
```

Sample success responses

`XML` format

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
                <Value>11.47</Value>
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
<RequestId>35D3E3DA-4650-407A-BFF5-59BFF1******</RequestId>
<EndTime>2020-09-23T01:01:00Z</EndTime>
<DBClusterId>pc-*****************</DBClusterId>
<StartTime>2020-09-23T01:00:00Z</StartTime>
<DBType>MySQL</DBType>
```

`JSON` format

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
                            "Value": "11.47",
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
    "RequestId": "35D3E3DA-4650-407A-BFF5-59BFF1******",
    "EndTime": "2020-09-23T01:01:00Z",
    "DBClusterId": "pc-*****************",
    "StartTime": "2020-09-23T01:00:00Z",
    "DBType": "MySQL"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/polardb).

