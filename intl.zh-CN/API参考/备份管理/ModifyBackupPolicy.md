# ModifyBackupPolicy {#reference_djb_dss_xfb .reference}

该接口用于修改自动备份策略。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyBackupPolicy。|
|DBClusterId|String|是|POLARDB集群ID。|
|PreferredBackupTime|String|是|自动备份时间（UTC时间），格式：*hh:mm*Z-*hh:mm*Z，必须为间隔1个小时的整点，例如14:00Z-15:00Z。|
|PreferredBackupPeriod|String|是|备份周期： -   Monday：周一
-   Tuesday：周二
-   Wednesday：周三
-   Thursday：周四
-   Friday：周五
-   Saturday：周六
-   Sunday：周日

 至少需要选择2天，多个值之间用英文逗号（,）隔开。

 |
|BackupRetentionPeriod|String|否|数据备份保留的天数，固定为7天，不可修改。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|请求ID。|

## 请求示例 {#section_snj_c3s_xfb .section}

``` {#codeblock_eiv_r3y_pb0}
https://polardb.aliyuncs.com/?Action=ModifyBackupPolicy
&DBClusterId=pc-bpxxxxxxx
&PreferredBackupTime=15:00Z-16:00Z
&PreferredBackupPeriod=Monday,Tuesday
&<公共请求参数>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_vya_f9a_0sc}
<ModifyBackupPolicyResponse>
<RequestId>C5A5DF0E-5968-4DC1-882E-AC2FE7067C88</RequestId>
</ModifyBackupPolicyResponse>
```

JSON格式

``` {#codeblock_w52_zes_68t}
{
    "RequestId":"C5A5DF0E-5968-4DC1-882E-AC2FE7067C88"
}
```

