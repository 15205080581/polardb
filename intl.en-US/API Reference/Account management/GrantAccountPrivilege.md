# GrantAccountPrivilege {#reference_ory_pbt_xfb .reference}

You can call this operation to grant access permissions on one or more databases in a specified ApsaraDB for POLARDB cluster to a database account. If the specified database account already has access permissions on one or more specified databases, the system directly returns a success response. Before you call this operation, ensure that the following requirement is met: The cluster must be in the running state.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to GrantAccountPrivilege.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to which a database account belongs.|
|AccountName|String|Yes|The name of the database account to be granted access permissions.|
|DBName|String|Yes|The name of the database whose access permissions are to be granted to the database account. You can grant access permissions on one or more databases to the database account. Separate multiple databases with a comma \(,\).

 |
|AccountPrivilege|String|Yes|The permissions of the database account on the database. Valid values: -   ReadWrite: has read and write permissions on the database.
-   ReadOnly: has the read-only permission on the database.
-   DMLOnly: runs only data manipulation language \(DML\) statements.
-   DDLOnly: runs only data definition language \(DDL\) statements.

 **Note:** The number of account permissions specified by the AccountPrivilege parameter must be the same as that of database names specified by the DBName parameter. Each account permission must correspond to a database name in sequence.

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=GrantAccountPrivilege
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&AccountName=testacc_01
&DBName=testdb_1
&AccountPrivilege=ReadOnly
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<GrantAccountPrivilegeResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</GrantAccountPrivilegeResponse>
```

JSON format

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

