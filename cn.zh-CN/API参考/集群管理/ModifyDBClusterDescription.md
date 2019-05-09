# ModifyDBClusterDescription {#reference_k3t_pns_xfb .reference}

该接口用于修改POLARDB集群的备注名，方便集群的维护。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyDBClusterDescription。|
|DBClusterId|String|是|集群ID。|
|DBClusterDescription|String|是|集群描述： -   以中文、英文字母开头；
-   可以包含中文、英文字符、数字、”\_”、” -”；
-   不能以http://，https开头；
-   长度为2-256个字符。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|RequestId。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ModifyDBClusterDescription
&DBClusterId=pc-xxxxxxxxxxxxxxxxx
&DBClusterDescription=ClusterDescriptionTest
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<ModifyDBClusterDescriptionResponse>  
	<RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</ModifyDBClusterDescriptionResponse>
```

JSON格式

```
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

