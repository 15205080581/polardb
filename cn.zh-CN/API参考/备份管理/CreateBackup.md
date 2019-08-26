# CreateBackup {#reference_vz4_14s_xfb .reference}

该接口用于手动为集群创建全量快照备份。

**说明：** 

-   每个集群最多可以同时存在3个手动创建的备份。如果已经存在3个手动创建的备份，需要先[删除备份](intl.zh-CN/API参考/备份管理/DeleteBackup.md#)，才能再手动创建备份。
-   调用该接口后，会在后台创建备份任务，若数据量较大，花费的时间可能较长，请耐心等待。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：CreateBackup。|
|DBClusterId|String|是|POLARDB集群ID。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|BackupJobId|String|备份集ID。|

## 请求示例 {#section_snj_c3s_xfb .section}

``` {#codeblock_ngf_tpu_6jj}
https://polardb.aliyuncs.com/?Action=CreateBackup
&DBClusterId=pc-bpxxxxxxx
&<公共请求参数>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_z2q_ov2_erv}
<CreateBackupResponse>
<RequestId>4F780C2E-163A-42C2-9D8A-B5A0C823B1DB</RequestId>
</CreateBackupResponse>
```

JSON格式

``` {#codeblock_ddr_97t_xav}
{
    "RequestId":"4F780C2E-163A-42C2-9D8A-B5A0C823B1DB"
}
```

