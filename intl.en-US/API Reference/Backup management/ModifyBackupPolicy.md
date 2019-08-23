# ModifyBackupPolicy {#reference_djb_dss_xfb .reference}

You can call this operation to modify the automatic backup policy of a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyBackupPolicy.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster whose automatic backup policy is to be modified.|
|PreferredBackupTime|String|Yes|The time for automatic backup. Specify the time in the *hh:mm*Z-*hh:mm*Z format, where the interval must be 1 hour and the start time and end time must be on the hour. The time must be in UTC. For example, 14:00Z-15:00Z.|
|PreferredBackupPeriod|String|Yes|The period of data backup. Valid values: -   Monday
-   Tuesday
-   Wednesday
-   Thursday
-   Friday
-   Saturday
-   Sunday

 Select at least two values. Separate multiple values with a comma \(,\).

 |
|BackupRetentionPeriod|String|No|The retention period of the backup data. Backup data is kept for 7 days by default. You cannot modify this value.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_snj_c3s_xfb .section}

``` {#codeblock_eiv_r3y_pb0}
https://polardb.aliyuncs.com/?Action=ModifyBackupPolicy
&DBClusterId=pc-bpxxxxxxx
&PreferredBackupTime=15:00Z-16:00Z
&PreferredBackupPeriod=Monday,Tuesday
&<Common request parameters>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_vya_f9a_0sc}
<ModifyBackupPolicyResponse>
<RequestId>C5A5DF0E-5968-4DC1-882E-AC2FE7067C88</RequestId>
</ModifyBackupPolicyResponse>
```

JSON format

``` {#codeblock_w52_zes_68t}
{
    "RequestId":"C5A5DF0E-5968-4DC1-882E-AC2FE7067C88"
}
```

