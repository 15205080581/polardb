# CloseDBClusterMigration {#reference_1392436 .reference}

该接口用于取消或完成迁移。

该接口用于RDS一键迁移到POLARDB时取消或完成迁移：

-   在切换前调用该接口会取消迁移；
-   在切换完成后调用该口会完成迁移。

详情请参见[一键升级RDS for MySQL到POLARDB for MySQL](../../../../intl.zh-CN/数据迁移__同步/POLARDB for MySQL/数据迁移/一键升级RDS for MySQL到POLARDB for MySQL.md#)。

调用该接口时，集群必须已经创建了一键升级任务。创建一键升级任务的接口为[CreateDBCluster](intl.zh-CN/API参考/集群管理/CreateDBCluster.md#)，参数**CreationOption**取值需要为**MigrationFromRDS**。

## 请求参数 {#section_tha_k9l_vae .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：CloseDBClusterMigration。|
|DBClusterId|String|是|POLARDB集群ID。|
|ContinueEnableBinlog|String|否|是否继续打开Binlog，取值： -   true：继续打开Binlog；
-   false：关闭Binlog。

 默认为true。 **说明：** 关闭Binlog将会重启您的POLARDB集群。

 |

## 返回参数 {#section_nkw_ki1_j6j .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|请求ID。|

## 请求示例 {#section_1m0_m44_kww .section}

``` {#codeblock_k0w_ks3_utb}
https://polardb.aliyuncs.com/?Action=CloseDBClusterMigration
&DBClusterId=pc-bpxxxxxxx
&<[公共请求参数]>
```

## 返回示例 {#section_t7z_2kd_sy2 .section}

XML格式

``` {#codeblock_ita_e8z_kjm}
<CloseDBClusterMigrationResponse>  
<RequestId>3AA69096-757C-4647-B36C-29EBC27A8763</RequestId>
</CloseDBClusterMigrationResponse>
```

JSON格式

``` {#codeblock_y3p_uvg_vc0}
{    "RequestId": "3AA69096-757C-4647-B36C-29EBC27A8763"}
```

