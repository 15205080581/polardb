# ModifyDBClusterMigration {#reference_1392435 .reference}

You can call this operation to modify a data migration task to complete it or roll it back.

When you migrate data from RDS to POLARDB with one click, you can call this operation to:

-   Migrate data from RDS to POLARDB before data migration.
-   Roll back data from POLARDB to RDS after data migration.

For more information, see [Upgrade RDS for MySQL to POLARDB for MySQL with one click](../../../../intl.en-US//Data migration/Upgrade RDS for MySQL to POLARDB for MySQL with one click.md#).

## Request parameters {#section_e8q_i5g_9xd .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyDBClusterMigration.|
|DBClusterId|String|Yes|The ID of the destination POLARDB cluster.|
|SourceRDSDBInstanceId|String|Yes|The ID of the source RDS instance.|
|NewMasterInstanceId|String|Yes|The ID of the new primary instance. Valid values: -   <DBClusterId\>: migrates data to the destination POLARDB cluster.
-   <SourceRDSDBInstanceId\>: rolls back data to the source RDS instance.

 |

## Response parameters {#section_nqz_4zk_by7 .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_tpc_p5a_qfk .section}

``` {#codeblock_iuj_dyu_i9u}
https://polardb.aliyuncs.com/?Action=ModifyDBClusterMigration
&DBClusterId=pc-bpxxxxxxx
&SourceRDSDBInstanceId=rm-bpxxxxxxx
&NewMasterInstanceId=pc-bpxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_mts_015_if9 .section}

XML format

``` {#codeblock_aaa_xhv_dsv}
<ModifyDBClusterMigrationResponse>  
<RequestId>A1B303A5-653F-4AEE-A598-023FF966C1E0</RequestId>
</ModifyDBClusterMigrationResponse>
```

JSON format

``` {#codeblock_3u9_nyf_11z}
{    "RequestId": "A1B303A5-653F-4AEE-A598-023FF966C1E0"}
```

