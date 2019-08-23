# DescribeBackupPolicy {#reference_bjk_sxs_xfb .reference}

该接口用于查看自动备份策略。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeBackupPolicy。|
|DBClusterId|String|是|POLARDB集群ID。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|BackupRetentionPeriod|Interger|数据备份保留的天数。|
|PreferredNextBackupTime|String|下一次备份的时间（UTC时间）。|
|PreferredBackupTime|String|自动备份时间（UTC时间）。|
|PreferredBackupPeriod|String|数据备份周期，取值： -   Monday：周一
-   Tuesday：周二
-   Wednesday：周三
-   Thursday：周四
-   Friday：周五
-   Saturday：周六
-   Sunday：周日

 |

## 请求示例 {#section_snj_c3s_xfb .section}

``` {#codeblock_6cz_l8s_gbo}
https://polardb.aliyuncs.com/?Action=DescribeBackupPolicy
&DBClusterId=pc-bpxxxxxxx
&<公共请求参数>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_bur_r3i_dqn}
<DescribeBackupPolicyResponse>
<PreferredBackupPeriod>Monday,Tuesday,Wednesday,Thursday,Friday,Saturday,Sunday</PreferredBackupPeriod>
    <RequestId>36590CA1-BAEE-4034-9CDD-33FFEC8C6BAE</RequestId>
    <PreferredBackupTime>14:00Z-15:00Z</PreferredBackupTime>
    <PreferredNextBackupTime>2019-07-27T14:32Z</PreferredNextBackupTime>
    <BackupRetentionPeriod>7</BackupRetentionPeriod>
</DescribeBackupPolicyResponse>
```

JSON格式

``` {#codeblock_80l_2ik_1dw}
{
    "PreferredBackupPeriod": "Monday,Tuesday,Wednesday,Thursday,Friday,Saturday,Sunday",
    "RequestId": "36590CA1-BAEE-4034-9CDD-33FFEC8C6BAE",
    "PreferredBackupTime": "14:00Z-15:00Z",
    "PreferredNextBackupTime": "2019-07-27T14:32Z",
    "BackupRetentionPeriod": 7
}
```

