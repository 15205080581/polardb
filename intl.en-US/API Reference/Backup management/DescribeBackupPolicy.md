# DescribeBackupPolicy {#reference_bjk_sxs_xfb .reference}

You can call this operation to query the automatic backup policy of a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeBackupPolicy.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to be queried.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|BackupRetentionPeriod|Integer|The retention period of the backup data.|
|PreferredNextBackupTime|String|The time for the next backup. The time is displayed in UTC.|
|PreferredBackupTime|String|The time for automatic backup. The time is displayed in UTC.|
|PreferredBackupPeriod|String|The period of data backup. Valid values: -   Monday
-   Tuesday
-   Wednesday
-   Thursday
-   Friday
-   Saturday
-   Sunday

 |

## Sample request {#section_snj_c3s_xfb .section}

``` {#codeblock_6cz_l8s_gbo}
https://polardb.aliyuncs.com/?Action=DescribeBackupPolicy
&DBClusterId=pc-bpxxxxxxx
&<Common request parameters>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_bur_r3i_dqn}
<DescribeBackupPolicyResponse>
<PreferredBackupPeriod>Monday,Tuesday,Wednesday,Thursday,Friday,Saturday,Sunday</PreferredBackupPeriod>
    <RequestId>36590CA1-BAEE-4034-9CDD-33FFEC8C6BAE</RequestId>
    <PreferredBackupTime>14:00Z-15:00Z</PreferredBackupTime>
    <PreferredNextBackupTime>2019-07-27T14:32Z</PreferredNextBackupTime>
    <BackupRetentionPeriod>7</BackupRetentionPeriod>
</DescribeBackupPolicyResponse>
```

JSON format

``` {#codeblock_80l_2ik_1dw}
{
    "PreferredBackupPeriod": "Monday,Tuesday,Wednesday,Thursday,Friday,Saturday,Sunday",
    "RequestId": "36590CA1-BAEE-4034-9CDD-33FFEC8C6BAE",
    "PreferredBackupTime": "14:00Z-15:00Z",
    "PreferredNextBackupTime": "2019-07-27T14:32Z",
    "BackupRetentionPeriod": 7
}
```

