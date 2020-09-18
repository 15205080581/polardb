# DescribeDBClusterMonitor

调用DescribeDBClusterMonitor接口查询PolarDB集群的监控数据采集频率。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=polardb&api=DescribeDBClusterMonitor&type=RPC&version=2017-08-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeDBClusterMonitor|系统规定参数，取值：**DescribeDBClusterMonitor**。 |
|DBClusterId|String|是|pc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|集群ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Period|String|60|监控数据的采集间隔，单位为秒。 |
|RequestId|String|593AE1C5-B70C-463F-9207-074639\*\*\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://polardb.aliyuncs.com/?Action=DescribeDBClusterMonitor
&DBClusterId=pc-****************
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RequestId>593AE1C5-B70C-463F-9207-074639******</RequestId>
<Period>60</Period>
```

`JSON` 格式

```
{
	"RequestId": "593AE1C5-B70C-463F-9207-074639******",
	"Period": "60"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/polardb)查看更多错误码。

