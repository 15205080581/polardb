# ModifyDBClusterMaintainTime {#reference_bkt_kjs_xfb .reference}

该接口用于修改POLARDB集群可例行维护的时间，一般设置为业务的低峰时间段。阿里云会在您设置的可维护时间段内进行集群维护，保证对业务的影响降到最低。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyDBClusterMaintainTime。|
|DBClusterId|String|是|集群ID。|
|MaintainTime|String|是|集群的可维护时间： 格式：*HH:mm*Z- *HH:mm*Z。

 示例：16:00Z-17:00Z，表示0点到1点\(UTC+08:00\)可进行例行维护。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ModifyDBClusterMaintainTime
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&MaintainTime=02:00Z-03:00Z
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<ModifyDBClusterMaintainTimeResponse>  
	<RequestId>70656639-1416-479F-AF13-D08197F9C43B</RequestId>
</ModifyDBClusterMaintainTimeResponse>
```

JSON格式

```
{
    "RequestId":"70656639-1416-479F-AF13-D08197F9C43B"
}
```

