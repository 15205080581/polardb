# DescribeAccounts {#reference_d5w_qzs_xfb .reference}

该接口用于查询POLARDB指定集群、指定数据库的账号列表信息或某个指定账号的信息。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeAccounts。|
|DBClusterId|String|是|集群ID。|
|AccountName|String|否|账号名。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)。|
|AccountList|List<DBAccount\>|账号组成的集合。|

## DBAccount参数 {#section_qgd_d1t_xfb .section}

|名称|类型|描述|
|--|--|--|
|AccountName|String|账号名。|
|AccountStatus|String|账号状态： -   Creating：创建中；
-   Available：可用；
-   Deleting：删除中。

 |
|AccountDescription|String|账号备注。|
|DatabasePrivileges|List<DatabasePrivilege\>|由DatabasePrivilege组成的数组。|
|AccountType|String|账户类型： -   Normal：普通账号；
-   Super：高权限账号。

 |

## DatabasePrivilege参数 {#section_lsg_chw_fgb .section}

|名称|类型|描述|
|:-|:-|:-|
|DBName|String|数据库名称。|
|AccountPrivilege|String|账号权限。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeAccounts
&DBClusterId=pc-xxxxxxxxxxxxxxx
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<DescribeAccountsResponse>  
	<Accounts>
		<DBInstanceAccount>
			<AccountStatus>0</AccountStatus>
			<AccountDescription></AccountDescription>
			<AccountName>testacc</AccountName>
			<DBClusterId>pc-xxxxxxxxxxxxxxxx</DBClusterId>
			<AccountType>Normal</AccountType>
		</DBInstanceAccount>
	</Accounts>
	<RequestId>16B29387-7226-4E6C-98C2-06B98FFD16D8</RequestId>
</DescribeAccountsResponse>
```

JSON格式

```
{
    "Accounts":{
        "DBInstanceAccount":[
            {
                "AccountStatus":"0",
                "AccountDescription":"",
                "AccountName":"testacc",
                "DBClusterId":"pc-xxxxxxxxxxxxxxx",
                "AccountType":"Normal"
            }
        ]
    },
    "RequestId":"16B29387-7226-4E6C-98C2-06B98FFD16D8"
}
```

