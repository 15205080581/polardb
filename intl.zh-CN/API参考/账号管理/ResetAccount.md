# ResetAccount {#concept_ymd_3bx_fgb .concept}

该接口用于重置POLARDB账号权限。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ResetAccount。|
|DBClusterId|String|是|集群ID。|
|AccountName|String|是|账号名。 **说明：** 仅支持重置高权限账号的权限。

 |
|AccountPassword|String|是|账号密码。 **说明：** 

-   大小写字母、数字、特殊字符占三种；
-   长度为8-32位；
-   特殊字符为!@\#$%^&\*\(\)\_+-=

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ResetAccount
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&AccountName=testacc
&AccountPassword=Pw123456
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<ResetAccountResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</ResetAccountResponse>
```

JSON格式

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

