# ModifyAccountDescription {#reference_yqb_s1t_xfb .reference}

该接口用于修改POLARDB数据库账号的备注信息。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyAccountDescription。|
|DBClusterId|String|是|集群ID。|
|AccountName|String|是|账号名。|
|AccountDescription|String|是|修改账号备注： -   以中文、英文字母开头；
-   可以包含中文、英文字符、数字、”\_”、” -”；
-   不能以http://，https:// 开头；
-   长度为2-256个字符。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ModifyAccountDescription
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&AccountName=testacc
&AccountDescription=AccDesc
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<ModifyAccountDescriptionResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</ModifyAccountDescriptionResponse>
```

JSON格式

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

