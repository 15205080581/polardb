# ModifyDBClusterMonitor

调用ModifyDBClusterMonitor接口修改PolarDB集群的监控数据采集频率。

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

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=polardb&api=ModifyDBClusterMonitor&type=RPC&version=2017-08-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|ModifyDBClusterMonitor|系统规定参数，取值：**ModifyDBClusterMonitor**。 |
|DBClusterId|String|是|pc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|集群ID。 |
|Period|String|是|5|监控的采集间隔，取值：

 -   5
-   60

 单位：秒。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|75B92353-73B4-447B-8477-C85F3C\*\*\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://polardb.aliyuncs.com/?Action=ModifyDBClusterMonitor
&DBClusterId=pc-****************
&Period=5
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RequestId>75B92353-73B4-447B-8477-C85F3C******</RequestId>
```

`JSON` 格式

```
{
	"RequestId": "75B92353-73B4-447B-8477-C85F3C******"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/polardb)查看更多错误码。

