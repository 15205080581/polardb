# CreateDatabase {#reference_ap4_bdt_xfb .reference}

You can call this operation to create a database for a specified ApsaraDB for POLARDB cluster.

## Description {#section_sxs_fps_xfb .section}

Before you call this operation, ensure that the following requirements are met:

-   The cluster must be in the running state.
-   The cluster cannot be locked.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to CreateDatabase.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster for which a database is to be created.|
|DBName|String|Yes|The name of the database to be created. The name must comply with the following rules: -   It must start with a lowercase letter and consist of lowercase letters, digits, hyphens \(-\), and underscores \(\_\).
-   It must end with a letter or a digit. It can be up to 64 characters in length.

 |
|CharacterSetName|String|Yes|The character set of the database. For more information, see [Character sets](intl.en-US/API Reference/Appendixes/Character sets.md#).|
|DBDescription|String|No|The description of the database. Valid values: -   It cannot start with http:// or https://.
-   It must be 2 to 256 characters in length.

 |
|AccountName|String|No|The name of the database account to be used.|
|AccountPrivilege|String|No|The permissions of the database account on the database. Valid values: -   ReadWrite: has read and write permissions on the database.
-   ReadOnly: has the read-only permission on the database.
-   DMLOnly: runs only data manipulation language \(DML\) statements.
-   DDLOnly: runs only data definition language \(DDL\) statements.
-   Default value: ReadWrite.

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=CreateDatabase
&DBClusterId=pc-xxxxxxxxxx
&CharacterSetName=utf8
&AccountName=testacc
&DBName=testDB
&AccountPrivilege=ReadWrite
&DBDescription=DBDesc
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<CreateDatabaseResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</CreateDatabaseResponse>
```

JSON format

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

