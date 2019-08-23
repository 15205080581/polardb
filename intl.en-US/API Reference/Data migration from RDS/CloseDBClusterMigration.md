# CloseDBClusterMigration {#reference_1392436 .reference}

You can call this operation to cancel or complete a data migration task.

When you migrate data from RDS to POLARDB with one click, you can call this operation to:

-   Cancel the migration task before data migration.
-   Complete the migration task after data migration.

For more information, see [Upgrade RDS for MySQL to POLARDB for MySQL with one click](../../../../intl.en-US//Data migration/Upgrade RDS for MySQL to POLARDB for MySQL with one click.md#).

## Request parameters {#section_tha_k9l_vae .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to CloseDBClusterMigration.|
|DBClusterId|String|Yes|The ID of the destination POLARDB cluster.|
|ContinueEnableBinlog|String|No|Specifies whether to continue to enable binary logs. Valid values: -   true: continues to enable binary logs.
-   false: disables binary logs.

 Default value: true. **Note:** If binary logs are disabled, your ApsaraDB for POLARDB cluster is restarted.

 |

## Response parameters {#section_nkw_ki1_j6j .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_1m0_m44_kww .section}

``` {#codeblock_k0w_ks3_utb}
https://polardb.aliyuncs.com/?Action=CloseDBClusterMigration
&DBClusterId=pc-bpxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_t7z_2kd_sy2 .section}

XML format

``` {#codeblock_ita_e8z_kjm}
<CloseDBClusterMigrationResponse>  
<RequestId>3AA69096-757C-4647-B36C-29EBC27A8763</RequestId>
</CloseDBClusterMigrationResponse>
```

JSON format

``` {#codeblock_y3p_uvg_vc0}
{    "RequestId": "3AA69096-757C-4647-B36C-29EBC27A8763"}
```

