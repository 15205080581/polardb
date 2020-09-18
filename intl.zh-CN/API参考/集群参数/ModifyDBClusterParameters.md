# ModifyDBClusterParameters

调用ModifyDBClusterParameters接口修改PolarDB集群的参数。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=polardb&api=ModifyDBClusterParameters&type=RPC&version=2017-08-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|ModifyDBClusterParameters|系统规定参数，取值为**ModifyDBClusterParameters**。 |
|DBClusterId|String|是|pc-xxxxxxxxxx|集群ID。 |
|Parameters|String|是|\{"auto\_increment\_increment":"1","character\_set\_filesystem":"utf8"\}|参数及其值的JSON串，参数的值都是字符串类型，例如`{"auto_increment_increment":"1","character_set_filesystem":"utf8"}`。

 **说明：** 您可以通过接口[DescribeDBClusterParameters](~~98122~~)查看PolarDB集群的参数。 |
|EffectiveTime|String|否|Auto|生效时间：

 -   **Auto**：自动判断修改的参数，如果不含需要重启的则立即生效，如果包含需要重启的，则全部放在可维护时间段内重启生效。
-   **Immediately**：立即生效。如果没有修改需要重启的参数，则无需重启立即生效；如果修改了需要重启的参数，则立即重启后生效。
-   **MaintainTime**：可维护时间段内生效。不论修改哪些参数，全放在可维护时间段内生效。

 默认为**Auto**。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|D0CEC6AC-7760-409A-A0D5-E6CD86\*\*\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://polardb.aliyuncs.com/?Action=ModifyDBClusterParameters
&DBClusterId=pc-xxxxxxxxxx
&Parameters={"auto_increment_increment":"1","character_set_filesystem":"utf8"} 
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyDBClusterParametersResponse>  
	  <RequestId>D0CEC6AC-7760-409A-A0D5-E6CD86******</RequestId>
</ModifyDBClusterParametersResponse>
```

`JSON` 格式

```
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD86******"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/polardb)查看更多错误码。

