# DescribeSQLExplorerRetention {#reference_spb_3lx_bgb .reference}

该接口用于查看集群的SQL审计保留策略。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeSQLExplorerRetention。|
|DBNodeId|String|否|节点ID。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|DBNodeId|String|节点ID。|
|ConfigValue|String|保留值。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeSQLExplorerPolicy
&DBInstanceId=xxxxxxxxxxxxx
&<公共请求参数>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<DescribeSQLExplorerRetentionResponse>
    <ConfigValue>30</ConfigValue>
	<DBInstanceID>10827789</DBInstanceID>
	<RequestId>483151A7-80C3-4420-836F-172E4597E2C8</RequestId>
	<DBInstanceName>pc-XXXXXXXXXX</DBInstanceName>
</DescribeSQLExplorerRetentionResponse>
```

JSON格式

```
{
    "ConfigValue":"30",
    "DBInstanceID":10827789,
    "RequestId":"483151A7-80C3-4420-836F-172E4597E2C8",
    "DBInstanceName":"pc-XXXXXXXXX"
}
```

