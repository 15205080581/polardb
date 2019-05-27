# CreateDatabase {#reference_ap4_bdt_xfb .reference}

该接口用于在POLARDB集群下创建一个新的数据库，

## 描述 {#section_sxs_fps_xfb .section}

集群必须满足以下条件，否则将创建失败：

-   当前集群状态：运行中；
-   当前集群锁定模式：正常。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：CreateDatabase。|
|DBClusterId|String|是|集群ID。|
|DBName|String|是|数据库名： -   以小写英文字母开头，由小写字母、数字、中划线、下划线组成；
-   字母或数字结尾，最长64个字符。

 |
|CharacterSetName|String|是|字符集，取值见[字符集表](cn.zh-CN/API参考/附表/字符集表.md#)。|
|DBDescription|String|否|数据库备注： -   不能以http://，https://开头；
-   长度为2-256个字符。

 |
|AccountName|String|否|账号名。|
|AccountPrivilege|String|否|账号权限： -   ReadWrite：读写；
-   ReadOnly：只读；
-   DMLOnly：只允许DML；
-   DDLOnly：只允许DDL；
-   不填默认为：ReadWrite。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=CreateDatabase
&DBClusterId=pc-xxxxxxxxxx
&CharacterSetName=utf8
&AccountName=testacc
&DBName=testDB
&AccountPrivilege=ReadWrite
&DBDescription=DBDesc
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<CreateDatabaseResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</CreateDatabaseResponse>
```

JSON格式

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

