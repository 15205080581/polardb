# RevokeAccountPrivilege {#reference_l3q_xbt_xfb .reference}

该接口用于删除POLARDB账号对数据库的访问权限。

## 描述 {#section_ucv_x1x_bgb .section}

集群必须满足以下条件，否则操作将失败：

-   集群状态为运行中；
-   数据库状态为运行中。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：RevokeAccountPrivilege。|
|DBClusterId|String|是|集群ID。|
|AccountName|String|是|账号名。|
|DBName|String|是|数据库名。多个数据库用英文逗号（,）分隔。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

``` {#codeblock_s01_rvv_8tj}
https://polardb.aliyuncs.com/?Action=RevokeAccountPrivilege
&DBClusterId=pc-xxxxxxxxxxxxxxx
&AccountName=testacc
&DBName=testDB
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_0be_gif_t7c}
<RevokeAccountPrivilegeResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</RevokeAccountPrivilegeResponse>
```

JSON格式

``` {#codeblock_gm1_rtx_2ce}
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

