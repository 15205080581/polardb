# DeleteBackup {#reference_jzv_tps_xfb .reference}

You can call this operation to delete the backup data of a specified ApsaraDB for POLARDB cluster.

Before you call this operation, ensure that the following requirements are met:

-   The cluster must be in the running state.
-   Data must be backed up.

    **Note:** You can call the [DescribeBackups](intl.en-US/API Reference/Backup management/DescribeBackups.md#) operation to query the backup status.


The space released after the backup file is deleted is much smaller than the size of this file due to the blocks shared between snapshots.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DeleteBackup.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster whose backup data is to be deleted.|
|BackupId|String|Yes|The ID of the backup. Separate multiple backup IDs with a comma. **Note:** You can call the [DescribeBackups](intl.en-US/API Reference/Backup management/DescribeBackups.md#) operation to query backup IDs.

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_snj_c3s_xfb .section}

``` {#codeblock_7ig_5j3_gos}
https://polardb.aliyuncs.com/?Action=DeleteBackup
&DBClusterId=pc-bpxxxxxxx
&BackupId=500018156
&<Common request parameters>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_91w_zmu_rfg}
<DeleteBackupResponse>
<RequestId>3CF4F9FE-BF77-4739-8D68-B8DF5D3BAD8B</RequestId>
</DeleteBackupResponse>
```

JSON format

``` {#codeblock_pes_0io_ilz}
{
    "RequestId":"3CF4F9FE-BF77-4739-8D68-B8DF5D3BAD8B"
}
```

