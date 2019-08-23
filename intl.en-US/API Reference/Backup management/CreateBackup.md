# CreateBackup {#reference_vz4_14s_xfb .reference}

You can call this operation to manually create a full snapshot backup for a specified ApsaraDB for POLARDB cluster.

**Note:** 

-   You can create up to three manual backups for each cluster. If three manual backups are created, you must [delete a backup](intl.en-US/API Reference/Backup management/DeleteBackup.md#) before manually creating one.
-   After you call this operation, a backup task is created in the background. It may take a long time to back up a large amount of data. Wait patiently.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to CreateBackup.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster whose data is to be backed up.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|

## Sample request {#section_snj_c3s_xfb .section}

``` {#codeblock_ngf_tpu_6jj}
https://polardb.aliyuncs.com/?Action=CreateBackup
&DBClusterId=pc-bpxxxxxxx
&<Common request parameters>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_z2q_ov2_erv}
<CreateBackupResponse>
<RequestId>4F780C2E-163A-42C2-9D8A-B5A0C823B1DB</RequestId>
</CreateBackupResponse>
```

JSON format

``` {#codeblock_ddr_97t_xav}
{
    "RequestId":"4F780C2E-163A-42C2-9D8A-B5A0C823B1DB"
}
```

