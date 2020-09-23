# ModifyDBClusterMonitor

Modifies the interval for collecting monitoring data of a PolarDB cluster.

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

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=polardb&api=ModifyDBClusterMonitor&type=RPC&version=2017-08-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|ModifyDBClusterMonitor|The operation that you want to perform. Set the value to **ModifyDBClusterMonitor**. |
|DBClusterId|String|Yes|pc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|The ID of the PolarDB cluster. |
|Period|String|Yes|5|The interval at which monitoring data is collected. Valid values:

 -   5
-   60

 Unit: seconds |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|75B92353-73B4-447B-8477-C85F3C\*\*\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://polardb.aliyuncs.com/? Action=ModifyDBClusterMonitor
&DBClusterId=pc-****************
&Period=5
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>75B92353-73B4-447B-8477-C85F3C******</RequestId>
```

`JSON` format

```
{
	"RequestId": "75B92353-73B4-447B-8477-C85F3C******"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/polardb).

