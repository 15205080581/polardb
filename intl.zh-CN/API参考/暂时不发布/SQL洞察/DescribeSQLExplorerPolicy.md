# DescribeSQLExplorerPolicy {#reference_uvw_4kx_bgb .reference}

该接口用于查看集群的SQL审计策略状态。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeSQLExplorerPolicy。|
|DBNodeId|String|否|节点ID。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](https://help.aliyun.com/document_detail/26224.html)。|
|SQLCollectorStatus|String|SQL审计状态：-   Enable：可用；
-   Disabled：不可用。

|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeSQLExplorerPolicy
&DBInstanceId=xxxxxxxxxxxxx
&<公共请求参数>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<DescribeSQLExplorerPolicyResponse>
    <RequestId>4F780C2E-163A-42C2-9D8A-B5A0C823B1DB</RequestId>
    <SQLCollectorStatus>Enable</SQLCollectorStatus>
</DescribeSQLExplorerPolicyResponse>
```

JSON格式

```
{
    "RequestId":"4F780C2E-163A-42C2-9D8A-B5A0C823B1DB",    
    "SQLCollectorStatus":"Enable"
}
```

