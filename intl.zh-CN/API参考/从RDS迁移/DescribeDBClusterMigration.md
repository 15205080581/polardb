# DescribeDBClusterMigration {#reference_1392434 .reference}

该接口用于查询POLARDB集群的迁移状态。

该接口用于查询RDS一键迁移到POLARDB的迁移状态。详情请参见[一键升级RDS for MySQL到POLARDB for MySQL](../../../../intl.zh-CN/数据迁移__同步/POLARDB for MySQL/数据迁移/一键升级RDS for MySQL到POLARDB for MySQL.md#)。

调用该接口时，集群必须已经创建了一键升级任务。创建一键升级任务的接口为[CreateDBCluster](intl.zh-CN/API参考/集群管理/CreateDBCluster.md#)，参数**CreationOption**取值需要为**MigrationFromRDS**。

## 请求参数 {#section_85h_fpg_ena .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeDBClusterMigration。|
|DBClusterId|String|是|POLARDB集群ID。|

## 返回参数 {#section_jjf_qn5_56d .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|DBClusterId|String|POLARDB集群ID。|
|SourceRDSDBInstanceId|String|源RDS实例ID。|
|RdsReadWriteMode|String|源RDS实例读写模式|
|DBClusterReadWriteMode|String|POLARDB集群读写模式。|
|MigrationStatus|String|迁移状态，取值： -   NO\_MIGRATION：没有迁移任务；
-   RDS2POLARDB\_CLONING：数据克隆中；
-   RDS2POLARDB\_SYNCING：数据同步中，此时POLARDB为只读，RDS为可读可写；
-   SWITCHING：数据库切换中；
-   POLARDB2RDS\_SYNCING：数据库切换完成，此时POLARDB为可读可写，RDS为只读。您可以修改应用内的连接地址；
-   ROLLBACK：迁移回滚中，回滚完成后，状态变更为RDS2POLARDB\_SYNCING；
-   CLOSING\_MIGRATION：关闭迁移任务中。

 |
|ReplicationInfo|JSON|同步链路的基本信息，取值： -   Topologies：同步关系。取值包含RDS2POLARDB（从RDS到POLARDB同步）和POLARDB2RDS（从POLARDB到RDS同步）；
-   DelayedSeconds：同步延迟时间，单位：秒；
-   ExpiredTime：到期时间，格式：*YYYY-MM-DD*T*hh:mm:ss*Z（UTC时间）。

 |

## 请求示例 {#section_rwd_ncl_dms .section}

``` {#codeblock_3ks_syr_fdq}
https://polardb.aliyuncs.com/?Action=DescribeDBClusterMigration
&DBClusterId=pc-bpxxxxxxx
&<[公共请求参数]>
```

## 返回示例 {#section_ms0_s7p_9yx .section}

XML格式

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

JSON格式

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

