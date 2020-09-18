# ModifyDBClusterParameters

Modifies the parameters of a specified PolarDB cluster.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=polardb&api=ModifyDBClusterParameters&type=RPC&version=2017-08-01)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|ModifyDBClusterParameters|The operation that you want to perform. Set the value to **ModifyDBClusterParameters**. |
|DBClusterId|String|Yes|pc-xxxxxxxxxx|The ID of the PolarDB cluster whose parameters are to be modified. |
|Parameters|String|Yes|\{"auto\_increment\_increment":"1","character\_set\_filesystem":"utf8"\}|The JSON string that consists of parameters and their values. The parameter values are strings, for example, `{"auto_increment_increment":"1","character_set_filesystem":"utf8"}`.

**Note:** You can call the [DescribeDBClusterParameters](~~98122~~) operation to view the parameters of the PolarDB cluster. |
|EffectiveTime|String|No|Auto|The time when the modified values of parameters take effect. Valid values:

-   **Auto**: The system automatically determines how the modified values of parameters take effect. If all the modified values of parameters can take effect regardless of a cluster restart, they immediately take effect. If a cluster restart is required to make the modified values of some parameters take effect, all of them take effect after a cluster restart within the maintenance window.
-   **Immediately**: If all the modified values of parameters can take effect regardless of a cluster restart, they immediately take effect. If a cluster restart is required to make the modified values of some parameters take effect, the cluster is immediately restarted to make all of them take effect.
-   **MaintainTime**: The modified values of parameters take effect within the maintenance window. Regardless of whether a cluster restart is required to make the modified values of parameters take effect, all of them take effect within the maintenance window.

Default value:**Auto** |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|D0CEC6AC-7760-409A-A0D5-E6CD86\*\*\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://polardb.aliyuncs.com/? Action=ModifyDBClusterParameters
&DBClusterId=pc-xxxxxxxxxx
&Parameters={"auto_increment":"1","character_set_filesystem":"utf8"} 
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDBClusterParametersResponse>  
      <RequestId>D0CEC6AC-7760-409A-A0D5-E6CD86******</RequestId>
</ModifyDBClusterParametersResponse>
```

`JSON` format

```
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD86******"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/polardb).

