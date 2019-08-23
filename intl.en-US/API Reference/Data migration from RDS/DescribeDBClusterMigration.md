# DescribeDBClusterMigration {#reference_1392434 .reference}

You can call this operation to query the data migration status of a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_85h_fpg_ena .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeDBClusterMigration.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to be queried.|

## Response parameters {#section_jjf_qn5_56d .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|DBClusterId|String|The ID of the ApsaraDB for POLARDB cluster.|
|SourceRDSDBInstanceId|String|The ID of the source RDS instance.|
|RdsReadWriteMode|String|The read/write mode of the source RDS instance.|
|DBClusterReadWriteMode|String|The read/write mode of the ApsaraDB for POLARDB cluster.|
|MigrationStatus|String|The status of the migration task. Valid values: -   NO\_MIGRATION: No migration task was running.
-   RDS2POLARDB\_CLONING: Data was being cloned.
-   RDS2POLARDB\_SYNCING: Data was being synchronized, during which the destination POLARDB cluster was in read-only mode and the source RDS instance was in read and write mode.
-   SWITCHING: Databases were being switched.
-   POLARDB2RDS\_SYNCING: Databases were switched. The destination POLARDB cluster was in read and write mode and the source RDS instance was in read-only mode. In this state, you can modify the connection points for your applications.
-   ROLLBACK: The migration task was rolling back, after which the value changed to RDS2POLARDB\_SYNCING.
-   CLOSING\_MIGRATION: The migration task was closing.

 |
|ReplicationInfo|JSON|The basic information about the data synchronization link. Valid values: -   Topologies: the synchronization path. Valid values: RDS2POLARDB, which indicates synchronization from RDS to POLARDB. POLARDB2RDS, which indicates synchronization from POLARDB to RDS.
-   DelayedSeconds: the synchronization latency, in seconds.
-   ExpiredTime: the expiration time. The time follows the ISO 8601 standard in the *yyyy-MM-dd*T*HH:mm:ss*Z format. The time is displayed in UTC.

 |

## Sample request {#section_rwd_ncl_dms .section}

``` {#codeblock_3ks_syr_fdq}
https://polardb.aliyuncs.com/?Action=DescribeDBClusterMigration
&DBClusterId=pc-bpxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_ms0_s7p_9yx .section}

XML format

``` {#codeblock_ocg_zr1_a6b}
<DescribeDBClusterMigrationResponse>  
     <Topologies>RDS2POLARDB</Topologies>
    <MigrationStatus>RDS2POLARDB_SYNCING</MigrationStatus>
    <RequestId>05B01253-7CE7-4192-ADBB-795564A90CAC</RequestId>
    <DBClusterId>pc-bpxxxxxxx</DBClusterId>
    <ExpiredTime></ExpiredTime>
    <RdsReadWriteMode>rw</RdsReadWriteMode>
    <DBClusterReadWriteMode>ro</DBClusterReadWriteMode>
    <DelayedSeconds>-1</DelayedSeconds>
    <SourceRDSDBInstanceId>rm-bpxxxxxxx</SourceRDSDBInstanceId>
</DescribeDBClusterMigrationResponse>
```

JSON format

``` {#codeblock_dj3_ma9_29o}
{
    "Topologies": "RDS2POLARDB",
    "MigrationStatus": "RDS2POLARDB_SYNCING",
    "RequestId": "05B01253-7CE7-4192-ADBB-795564A90CAC",
    "DBClusterId": "pc-bpxxxxxxx",
    "ExpiredTime": "",
    "RdsReadWriteMode": "rw",
    "DBClusterReadWriteMode": "ro",
    "DelayedSeconds": -1,
    "SourceRDSDBInstanceId": "rm-bpxxxxxxx"
}
```

