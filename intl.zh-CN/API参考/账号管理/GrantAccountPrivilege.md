# GrantAccountPrivilege {#reference_ory_pbt_xfb .reference}

该接口用于授权账号访问POLARDB集群的某个数据库，一个账号可关联一个或多个数据库。如果指定的账号对指定数据库已经具有访问权限，则会直接返回成功。集群状态为运行中，否则操作将失败。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：GrantAccountPrivilege。|
|DBClusterId|String|是|集群ID。|
|AccountName|String|是|账号名。|
|DBName|String|是|设置要授权的数据库名。 支持同时对一个或多个数据库授权，多个数据库之间用英文","隔开。

 |
|AccountPrivilege|String|是|账号权限： -   ReadWrite：读写；
-   ReadOnly：只读；
-   DMLOnly：只允许DML；
-   DDLOnly：只允许DDL。

 **说明：** AccountPrivilege的个数需要与DBName保持一致，且顺序对应。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=GrantAccountPrivilege
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&AccountName=testacc_01
&DBName=testdb_1
&AccountPrivilege=ReadOnly
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<GrantAccountPrivilegeResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</GrantAccountPrivilegeResponse>
```

JSON格式

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

