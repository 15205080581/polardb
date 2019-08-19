# DescribeBackups {#reference_c11_hqs_xfb .reference}

You can call this operation to query the backup data of a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeBackups.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to be queried.|
|BackupId|String|No|The ID of the backup to be queried.|
|BackupStatus|String|No|The status of the backup task. Valid values: -   Success: The backup task is completed.
-   Failed: The backup task failed.

 |
|BackupMode|String|No|The mode of the backup. Valid values: -   Automated: automatic backup
-   Manual: manual backup

 |
|StartTime|String|Yes|The beginning of the time range where the backup data is queried. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC.|
|EndTime|String|Yes|The end of the time range where the backup data is queried. The end time must be later than the start time. Specify the time in the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm*Z format. The time must be in UTC.|
|PageSize|Integer|No|The number of entries to return on each page. Valid values: -   30
-   50
-   100

 Default value: 30.

 |
|PageNumber|Integer|No|The number of the page to return. Valid values: any non-zero positive integer. Default value: 1.

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|TotalRecordCount|String|The total number of entries returned.|
|PageNumber|String|The number of the page returned.|
|PageRecordCount|String|The total number of pages returned.|
|Items|List<Backup\>|The list of backups.|

## Backup {#section_qym_brs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|BackupId|String|The ID of the backup.|
|DBClusterId|String|The ID of the ApsaraDB for POLARDB cluster.|
|BackupStatus|String|The status of the backup task. Valid values: -   Success: The backup task is completed.
-   Failed: The backup task failed.

 |
|BackupStartTime|String|The time when this backup task started. The time is displayed in UTC.|
|BackupEndTime|String|The time when this backup task ended. The time is displayed in UTC.|
|BackupMode|String|The mode of the backup. Valid values: -   Automated: automatic backup
-   Manual: manual backup

 |
|BackupMethod|String|The method of the backup. Currently, only snapshot backup is supported. The value is Snapshot.|
|BackupType|String|The type of the backup. Currently, only full backup is supported. The value is FullBackup.|
|BackupConsistentTime|String|The time point of consistent backup, that is, the time when data was backed up.|
|BackupSize|String|The size of the backup file, in bytes. **Note:** The space released after the backup file is deleted is much smaller than the size of this file due to the blocks shared between snapshots.

 |

## Sample request {#section_snj_c3s_xfb .section}

``` {#codeblock_ul3_td4_14t}
https://polardb.aliyuncs.com/?Action=DescribeBackups
&DBClusterId=pc-bpxxxxxxx
&StartTime=2019-07-26T15:00Z
&EndTime=2019-07-27T15:00Z
&<Common request parameters>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_gn0_799_cxb}
<DescribeBackupsResponse>
<Items>
        <Backup>
            <StoreStatus>Enabled</StoreStatus>
            <BackupType>FullBackup</BackupType>
            <BackupEndTime>2019-07-27T07:31:23Z</BackupEndTime>
            <BackupMethod>Snapshot</BackupMethod>
            <BackupMode>Manual</BackupMode>
            <BackupStatus>Success</BackupStatus>
            <DBClusterId>pc-bpxxxxxxx</DBClusterId>
            <BackupStartTime>2019-07-27T07:31:13Z</BackupStartTime>
            <BackupId>423957113</BackupId>
        </Backup>
        <Backup>
            <StoreStatus>Enabled</StoreStatus>
            <BackupType>FullBackup</BackupType>
            <BackupEndTime>2019-07-27T07:27:18Z</BackupEndTime>
            <BackupMethod>Snapshot</BackupMethod>
            <BackupMode>Manual</BackupMode>
            <BackupStatus>Success</BackupStatus>
            <DBClusterId>pc-bpxxxxxxx</DBClusterId>
            <BackupStartTime>2019-07-27T07:27:08Z</BackupStartTime>
            <BackupId>423955591</BackupId>
        </Backup>
    </Items>
    <PageNumber>1</PageNumber>
    <TotalRecordCount>2</TotalRecordCount>
    <RequestId>E22FB172-F0AB-42FF-A6D0-115065D64971</RequestId>
    <PageRecordCount>2</PageRecordCount>
</DescribeBackupsResponse>
```

JSON format

``` {#codeblock_upn_uof_oz3}
{
    "Items": {
        "Backup": [
            {
                "StoreStatus": "Enabled",
                "BackupType": "FullBackup",
                "BackupEndTime": "2019-07-27T07:31:23Z",
                "BackupMethod": "Snapshot",
                "BackupMode": "Manual",
                "BackupStatus": "Success",
                "DBClusterId": "pc-bpxxxxxxx",
                "BackupStartTime": "2019-07-27T07:31:13Z",
                "BackupId": 423957113
            },
            {
                "StoreStatus": "Enabled",
                "BackupType": "FullBackup",
                "BackupEndTime": "2019-07-27T07:27:18Z",
                "BackupMethod": "Snapshot",
                "BackupMode": "Manual",
                "BackupStatus": "Success",
                "DBClusterId": "pc-bpxxxxxxx",
                "BackupStartTime": "2019-07-27T07:27:08Z",
                "BackupId": 423955591
            },
        ]
    },
    "PageNumber": 1,
    "TotalRecordCount": 2,
    "RequestId": "E22FB172-F0AB-42FF-A6D0-115065D64971",
    "PageRecordCount": 2
}
```

