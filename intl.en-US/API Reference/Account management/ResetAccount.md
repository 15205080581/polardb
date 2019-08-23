# ResetAccount {#concept_ymd_3bx_fgb .concept}

You can call this operation to reset the permissions of a database account for a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ResetAccount.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to which a database account belongs.|
|AccountName|String|Yes|The name of the database account whose permissions are to be reset. **Note:** You can reset only the permissions of a privileged account.

 |
|AccountPassword|String|Yes|The password of the database account whose permissions are to be reset. **Note:** 

-   The password must consist of any three types of characters, including uppercase letters, lowercase letters, digits, and special characters.
-   It must be 8 to 32 characters in length.
-   Special characters include exclamation points \(!\), at signs \(@\), number signs \(\#\), dollar signs \($\), percent signs \(%\), carets \(^\), ampersands \(&\), asterisks \(\*\), parentheses \(\(\)\), underscores \(\_\), plus signs \(+\), hyphens \(-\), and equal signs \(=\).

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ResetAccount
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&AccountName=testacc
&AccountPassword=Pw123456
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<ResetAccountResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</ResetAccountResponse>
```

JSON format

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

