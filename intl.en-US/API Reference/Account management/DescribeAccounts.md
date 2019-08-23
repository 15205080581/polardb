# DescribeAccounts {#reference_d5w_qzs_xfb .reference}

You can call this operation to query the database accounts or a specified database account of a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeAccounts.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to be queried.|
|AccountName|String|No|The name of the database account to be queried.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|AccountList|List<DBAccount\>|The list of database accounts.|

## DBAccount {#section_qgd_d1t_xfb .section}

|Parameter|Type|Description|
|---------|----|-----------|
|AccountName|String|The name of the database account.|
|AccountStatus|String|The status of the database account. Valid values: -   Creating: The account is being created.
-   Available: The account is available.
-   Deleting: The account is being deleted.

 |
|AccountDescription|String|The description of the database account.|
|DatabasePrivileges|List<DatabasePrivilege\>|The list of database account permissions.|
|AccountType|String|The type of the database account. Valid values: -   Normal: standard account
-   Super: privileged account

 |

## DatabasePrivilege {#section_lsg_chw_fgb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|DBName|String|The name of the database.|
|AccountPrivilege|String|The permissions of the database account on the database.|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeAccounts
&DBClusterId=pc-xxxxxxxxxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

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

JSON format

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

