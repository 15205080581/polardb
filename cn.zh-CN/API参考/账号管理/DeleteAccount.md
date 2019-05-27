# DeleteAccount {#reference_gxs_jbt_xfb .reference}

该接口用于删除POLARDB数据库账号。

## 描述 {#section_ucv_x1x_bgb .section}

集群状态必须为运行中，否则操作将失败。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DeleteAccount。|
|DBClusterId|String|是|集群ID。|
|AccountName|String|是|账号名。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=CreateAccount
&DBClusterId=pc-xxxxxxxxxxxxxxxxxxx
&AccountName=testacc
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<DeleteAccountResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</DeleteAccountResponse>
```

JSON格式

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

