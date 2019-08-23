# ModifyAutoRenewAttribute {#reference_220995 .reference}

该接口用于设置POLARDB包年包月集群自动续费状态。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyAutoRenewAttribute。|
|DBClusterIds|String|是|数据库集群ID。|
|RegionId|String|是|地域ID，长度不超过50个字符，通过接口[DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#)查看可用的地域。|
|RenewalStatus|String|否|设置自动续费状态： -   AutoRenewal：自动续费；
-   Normal：手动续费；
-   NotRenewal：不再续费。

 默认为AutoRenewal。

 **说明：** 设置为NotRenewal后，系统不再发送到期提醒，只在到期前第三天发送不续费提醒。

 |
|PeriodUnit|String|否|续费时长的单位： -   Year：年；
-   Month：月。

 默认为Month。

 |
|Duration|String|否|设置集群自动续费时长： -   当PeriodUnit为Month时，取值为\[1,2,3,6,12\]；
-   当PeriodUnit为Year时，取值为\[1-3\]。

 默认为1。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

``` {#codeblock_d61_8jy_8w5}
https://polardb.aliyuncs.com/?Action=ModifyAutoRenewAttribute
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&RegionId=cn-hangzhou
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_yvz_xav_wi4}
<ModifyAutoRenewAttributeResponse>  
    <RequestId>4CE6DF97-AEA4-484F-906F-C407EE3770EB</RequestId>
</ModifyAutoRenewAttributeResponse>
```

JSON格式

``` {#codeblock_0kn_qly_81g}
{
    "RequestId": "4CE6DF97-AEA4-484F-906F-C407EE3770EB"
}
```

