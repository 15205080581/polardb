# DeleteBackup {#reference_jzv_tps_xfb .reference}

该接口用于删除备份。

集群必须满足以下条件，否则将导致删除失败：

-   集群状态为运行中；
-   备份状态为已完成。

    **说明：** 可以通过[DescribeBackups](intl.zh-CN/API参考/备份管理/DescribeBackups.md#)接口查询备份状态。


删除备份后释放的空间远小于该备份文件的大小，因为快照之间有共享的数据块。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DeleteBackup。|
|DBClusterId|String|是|POLARDB集群ID。|
|BackupId|String|是|备份ID，多个备份之间用英文逗号（,）分隔。 **说明：** 您可以通过[DescribeBackups](intl.zh-CN/API参考/备份管理/DescribeBackups.md#)接口查询BackupId。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|请求ID。|

## 请求示例 {#section_snj_c3s_xfb .section}

``` {#codeblock_7ig_5j3_gos}
https://polardb.aliyuncs.com/?Action=DeleteBackup
&DBClusterId=pc-bpxxxxxxx
&BackupId=500018156
&<公共请求参数>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_91w_zmu_rfg}
<DeleteBackupResponse>
<RequestId>3CF4F9FE-BF77-4739-8D68-B8DF5D3BAD8B</RequestId>
</DeleteBackupResponse>
```

JSON格式

``` {#codeblock_pes_0io_ilz}
{
    "RequestId":"3CF4F9FE-BF77-4739-8D68-B8DF5D3BAD8B"
}
```

