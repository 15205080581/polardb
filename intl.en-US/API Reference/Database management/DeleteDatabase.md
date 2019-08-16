# DeleteDatabase {#reference_psk_fft_xfb .reference}

You can call this operation to delete a database for a specified ApsaraDB for POLARDB cluster.

## Description {#section_sxs_fps_xfb .section}

Before you call this operation, ensure that the following requirements are met:

-   The cluster must be in the running state.
-   The cluster cannot be locked.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DeleteDatabase.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to which a database belongs.|
|DBName|String|Yes|The name of the database to be deleted.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DeleteDatabase
&DBClusterId=pc-xxxxxxxxxx
&DBName=testDB
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<DeleteDatabaseResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</DeleteDatabaseResponse>
```

JSON format

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

