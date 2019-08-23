# DescribeBackups {#reference_c11_hqs_xfb .reference}

该接口用于查询集群的备份信息。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeBackups。|
|DBClusterId|String|是|POLARDB集群ID。|
|BackupId|String|否|备份ID。|
|BackupStatus|String|否|备份状态，取值： -   Success：备份完成；
-   Failed：备份失败。

 |
|BackupMode|String|否|备份类型，取值： -   Automated：系统自动备份；
-   Manual：手动备份。

 |
|StartTime|String|是|查询开始时间。格式：*YYYY-MM-DD*T*hh:mm*Z（UTC时间）。|
|EndTime|String|是|查询结束时间，需晚于查询开始时间。格式：*YYYY-MM-DD*T*hh:mm*Z（UTC时间）。|
|PageSize|Integer|否|每页记录数，取值： -   30；
-   50；
-   100。

 默认值：30。

 |
|PageNumber|Integer|否|页码，大于0且不超过Integer的最大值。 默认值：1。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|TotalRecordCount|String|总记录数。|
|PageNumber|String|页码。|
|PageRecordCount|String|本页记录数。|
|Items|List<Backup\>|由备份组成的列表。|

## Backup参数 {#section_qym_brs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|BackupId|String|备份ID。|
|DBClusterId|String|POLARDB集群ID。|
|BackupStatus|String|备份状态，取值： -   Success：备份已完成；
-   Failed：备份失败。

 |
|BackupStartTime|String|本次备份开始时间（UTC时间）。|
|BackupEndTime|String|本次备份结束时间（UTC时间）。|
|BackupMode|String|备份类型，取值： -   Automated：系统自动备份；
-   Manual：手动备份。

 |
|BackupMethod|String|备份方式，仅支持快照备份，取值：Snapshot 。|
|BackupType|String|备份种类，仅支持全量备份，取值：FullBackup。|
|BackupConsistentTime|String|一致性备份时间点，即备份中数据的时间点。|
|BackupSize|String|备份文件大小，单位：Byte。 **说明：** 删除该快照备份后释放的空间远小于该备份文件的大小，因为快照之间有共享的数据块。

 |

## 请求示例 {#section_snj_c3s_xfb .section}

``` {#codeblock_ul3_td4_14t}
https://polardb.aliyuncs.com/?Action=DescribeBackups
&DBClusterId=pc-bpxxxxxxx
&StartTime=2019-07-26T15:00Z
&EndTime=2019-07-27T15:00Z
&<公共请求参数>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

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

JSON格式

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

