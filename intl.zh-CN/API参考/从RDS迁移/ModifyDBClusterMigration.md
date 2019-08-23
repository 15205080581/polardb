# ModifyDBClusterMigration {#reference_1392435 .reference}

该接口用于修改迁移任务，进行任务的切换或回滚。

该接口用于RDS一键迁移到POLARDB时进行切换或回滚：

-   在切换前调用该接口会进行切换；
-   在切换完成后调用该口会进行回滚。

详情请参见[一键升级RDS for MySQL到POLARDB for MySQL](../../../../intl.zh-CN/数据迁移__同步/POLARDB for MySQL/数据迁移/一键升级RDS for MySQL到POLARDB for MySQL.md#)。

调用该接口时，集群必须已经创建了一键升级任务。创建一键升级任务的接口为[CreateDBCluster](intl.zh-CN/API参考/集群管理/CreateDBCluster.md#)，参数**CreationOption**取值需要为**MigrationFromRDS**。

## 请求参数 {#section_e8q_i5g_9xd .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyDBClusterMigration。|
|DBClusterId|String|是|POLARDB集群ID。|
|SourceRDSDBInstanceId|String|是|源RDS实例ID。|
|NewMasterInstanceId|String|是|新的主实例ID，取值： -   <DBClusterId\>：填写POLARDB集群ID时进行切换。
-   <SourceRDSDBInstanceId\>：切换后，可以填写RDS实例ID时进行回滚。

 |

## 返回参数 {#section_nqz_4zk_by7 .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|请求ID。|

## 请求示例 {#section_tpc_p5a_qfk .section}

``` {#codeblock_iuj_dyu_i9u}
https://polardb.aliyuncs.com/?Action=ModifyDBClusterMigration
&DBClusterId=pc-bpxxxxxxx
&SourceRDSDBInstanceId=rm-bpxxxxxxx
&NewMasterInstanceId=pc-bpxxxxxxx
&<[公共请求参数]>
```

## 返回示例 {#section_mts_015_if9 .section}

XML格式

``` {#codeblock_aaa_xhv_dsv}
<ModifyDBClusterMigrationResponse>  
<RequestId>A1B303A5-653F-4AEE-A598-023FF966C1E0</RequestId>
</ModifyDBClusterMigrationResponse>
```

JSON格式

``` {#codeblock_3u9_nyf_11z}
{    "RequestId": "A1B303A5-653F-4AEE-A598-023FF966C1E0"}
```

