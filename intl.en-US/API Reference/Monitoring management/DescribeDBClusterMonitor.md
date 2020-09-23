# DescribeDBClusterMonitor

Queries the interval for collecting monitoring data of a PolarDB cluster.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=polardb&api=DescribeDBClusterMonitor&type=RPC&version=2017-08-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|DescribeDBClusterMonitor|The operation that you want to perform. Set the value to **DescribeDBClusterMonitor**. |
|DBClusterId|String|Yes|pc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|The ID of the PolarDB cluster. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Period|String|60|The interval at which monitoring data is collected. Unit: seconds. |
|RequestId|String|593AE1C5-B70C-463F-9207-074639\*\*\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://polardb.aliyuncs.com/? Action=DescribeDBClusterMonitor
&DBClusterId=pc-****************
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>593AE1C5-B70C-463F-9207-074639******</RequestId>
<Period>60</Period>
```

`JSON` format

```
{
	"RequestId": "593AE1C5-B70C-463F-9207-074639******",
	"Period": "60"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/polardb).

