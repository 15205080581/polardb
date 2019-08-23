# ModifyDBClusterParameters {#reference_zst_xgt_xfb .reference}

该接口用于修改POLARDB集群的参数。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyDBClusterParameters。|
|DBClusterId|String|是|集群ID。|
|Parameters|String|是|参数及其值的JSON串，参数的值都是字符串类型： \{"auto\_increment":"1","character\_set\_client":"utf8"\}

 |
|EffectiveTime|String|否|生效时间： -   Auto：自动判断修改的参数，如果不含需要重启的则立即生效，如果包含需要重启的，则全部放在可维护时间段内重启生效。
-   Immediately：立即生效。如果没有修改需要重启的参数，则无需重启立即生效；如果修改了需要重启的参数，则立即重启后生效。
-   MaintainTime：可维护时间段内生效。不论修改哪些参数，全放在可维护时间段内生效。

 默认为Auto。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>| |详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|RequestId。|

## 请求示例 {#section_khc_1dz_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ModifyDBClusterParameters
&DBClusterId=pc-xxxxxxxxxx
&Parameters= {"auto_increment":"1","character_set_client":"utf8"}
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<ModifyDBClusterParametersResponse>  
	<RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</ModifyDBClusterParametersResponse>
```

JSON格式

```
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

