# CreateAccount {#reference_lsd_pys_xfb .reference}

You can call this operation to create a database account for a specified ApsaraDB for POLARDB cluster.

## Description {#section_qhc_1xw_bgb .section}

Before you call this operation, ensure that the following requirements are met:

-   The cluster must be in the running state.
-   Databases must be in the running state.
-   The cluster cannot be locked.
-   The number of database accounts in the cluster cannot exceed the upper limit.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to CreateAccount.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster for which a database account is to be created.|
|AccountName|String|Yes|The name of the database account. The name must comply with the following rules: -   It must start with a lowercase letter and consist of lowercase letters, digits, and underscores \(\_\).
-   It can be up to 16 characters in length.

 |
|AccountPassword|String|Yes|The password of the database account. The password must comply with the following rules: -   It must consist of uppercase letters, lowercase letters, digits, and special characters. Special characters include exclamation points \(!\), number signs \(\#\), dollar signs \($\), percent signs \(%\), carets \(^\), ampersands \(&\), asterisks \(\*\), parentheses \(\(\)\), underscores \(\_\), plus signs \(+\), hyphens \(-\), and equal signs \(=\).
-   It must be 8 to 32 characters in length.

 |
|AccountType|String|No|The type of the database account. Valid values: -   Normal: standard account
-   Super: privileged account
-   Default value: Super.

 For more information about how to create a database account, click [here](../../../../intl.en-US/.md#).

 **Note:** 

-   Currently, POLARDB for PostgreSQL and POLARDB for Oracle do not support standard accounts.
-   You can create only one privileged account for an ApsaraDB for POLARDB cluster.

 |
|DBName|String|No|The name of the database whose access permissions are to be granted to the database account. Separate multiple databases with a comma \(,\).|
|AccountPrivilege|String|No|The permissions of the database account on the database. Valid values: -   ReadWrite: has read and write permissions on the database.
-   ReadOnly: has the read-only permission on the database.
-   DMLOnly: runs only data manipulation language \(DML\) statements.
-   DDLOnly: runs only data definition language \(DDL\) statements.
-   Default value: ReadWrite.

 |
|AccountDescription|String|No|The description of the database account. The description must comply with the following rules: -   It cannot start with http:// or https://.
-   It must be 2 to 256 characters in length.

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|

## Sample request {#section_snj_c3s_xfb .section}

``` {#codeblock_wzx_vgg_ua7}
https://polardb.aliyuncs.com/?Action=CreateAccount
&DBClusterId=pc-xxxxxxxxxxxxxxx
&AccountName=testacc
&AccountPassword=Pw123456
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_eru_488_uwa}
<CreateAccountResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</CreateAccountResponse>
```

JSON format

``` {#codeblock_om1_xoj_hr7}
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

