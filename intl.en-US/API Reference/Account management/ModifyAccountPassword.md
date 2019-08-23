# ModifyAccountPassword {#reference_hqc_dbt_xfb .reference}

You can call this operation to change the password of a database account for a specified ApsaraDB for POLARDB cluster.

## Description {#section_otn_vzw_bgb .section}

Before you call this operation, ensure that the following requirements are met:

-   The cluster must be in the running state.
-   The cluster cannot be locked.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyAccountPassword.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to which a database account belongs.|
|AccountName|String|Yes|The name of the database account whose password is to be changed.|
|AccountPassword|String|Yes|The password of the database account.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ResetAccountPassword
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&AccountName=testacc
&AccountPassword=Pw123456
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<ResetAccountPasswordResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</ResetAccountPasswordResponse>
```

JSON format

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

