# CreateAccount {#reference_lsd_pys_xfb .reference}

该接口用于为POLARDB数据库创建账号。

## 描述 {#section_qhc_1xw_bgb .section}

集群和数据库必须满足以下条件，否则将创建失败：

-   当前集群状态为运行中；
-   当前数据库状态为运行中；
-   当前集群没有被锁定；
-   没有超出单个集群内的最大账号数量。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：CreateAccount。|
|DBClusterId|String|是|集群ID。|
|AccountName|String|是|账号名： -   由小写字母，数字、下划线组成，小写字母开头；
-   长度不超过16个字符。

 |
|AccountPassword|String|是|账号密码： -   由大写字母、小写字母、数字、特殊字符组成（特殊字符为!\#$%^&\*\(\)\_+-=）；
-   长度为8-32位。

 |
|AccountType|String|否|账号类型： -   Normal：普通账号；
-   Super：高权限账号；
-   不填默认为：Super。

 创建数据库账号详情见[这里](../../../../cn.zh-CN/快速入门/创建数据库账号.md#)。

 **说明：** 

-   POLARDB for PostgreSQL/Oracle暂不支持创建普通账号。
-   每个POLARDB集群最多只允许创建1个高权限账号。

 |
|DBName|String|否|数据库名，多个以’,’分隔。|
|AccountPrivilege|String|否|账号权限： -   ReadWrite：读写；
-   ReadOnly：只读 ；
-   DMLOnly：只允许DML；
-   DDLOnly：只允许DDL；
-   不填默认为：ReadWrite。

 |
|AccountDescription|String|否|修改账号备注： -   不能以http://，https:// 开头；
-   长度为2-256个字符。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=CreateAccount
&DBClusterId=pc-xxxxxxxxxxxxxxx
&AccountName=testacc
&AccountPassword=Pw123456
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<CreateAccountResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</CreateAccountResponse>
```

JSON格式

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

