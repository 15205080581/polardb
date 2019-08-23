# ModifySQLExplorerPolicy {#reference_dcg_sjx_bgb .reference}

该接口用于切换集群的SQL采集状态。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifySQLExplorerPolicy。|
|DBNodeId|String|否|节点ID。|
|SQLCollectorStatus|String|是|SQL采集状态：-   Enable：开启；
-   Disabled：关闭。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ModifySQLExplorerPolicy
&DBInstanceId=xxxxxxxxxxxx
&SQLCollectorStatus=Disabled
&<公共请求参数>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<ModifySQLExplorerPolicyResponse>
    <RequestId>4F780C2E-163A-42C2-9D8A-B5A0C823B1DB</RequestId>
</ModifySQLExplorerPolicyResponse>
```

JSON格式

```
{
    "RequestId":"4F780C2E-163A-42C2-9D8A-B5A0C823B1DB"
}
```

