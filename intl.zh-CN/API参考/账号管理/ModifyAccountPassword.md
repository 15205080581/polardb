# ModifyAccountPassword {#reference_hqc_dbt_xfb .reference}

该接口用于修改POLARDB数据库的账号密码。

## 描述 {#section_otn_vzw_bgb .section}

必须满足以下条件，否则将操作失败：

-   当前集群状态为运行中；
-   没有被锁定。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyAccountPassword。|
|DBClusterId|String|是|集群ID。|
|AccountName|String|是|账号名。|
|AccountPassword|String|是|账号密码。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ResetAccountPassword
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&AccountName=testacc
&AccountPassword=Pw123456
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<ResetAccountPasswordResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</ResetAccountPasswordResponse>
```

JSON格式

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

