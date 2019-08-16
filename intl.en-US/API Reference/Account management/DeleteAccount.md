# DeleteAccount {#reference_gxs_jbt_xfb .reference}

You can call this operation to delete a database account for a specified ApsaraDB for POLARDB cluster.

## Description {#section_ucv_x1x_bgb .section}

Before you call this operation, ensure that the following requirement is met: The cluster must be in the running state.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DeleteAccount.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to which a database account belongs.|
|AccountName|String|Yes|The name of the database account to be deleted.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=CreateAccount
&DBClusterId=pc-xxxxxxxxxxxxxxxxxxx
&AccountName=testacc
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<DeleteAccountResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</DeleteAccountResponse>
```

JSON format

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

