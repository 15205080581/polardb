# ModifyDBDescription {#concept_h3q_rfd_ggb .concept}

该接口用于修改POLARDB数据库的描述或备注信息。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyDBDescription。|
|DBClusterId|String|是|集群ID。|
|DBName|String|是|数据库名。|
|DBDescription|String|是|数据库备注。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ModifyDBDescription
&DBClusterId=pc-xxxxxxxxxxxxxxxxxxxx
&DBName=testDB
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<CheckDBNameResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</CheckDBNameResponse>
```

JSON格式

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

