# DeleteDBCluster {#reference_afp_n25_xfb .reference}

该接口用于删除POLARDB集群。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DeleteDBCluster。|
|DBClusterId|String|是|集群ID。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|requestId。|

## 请求示例 {#section_lx1_c25_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DeleteDBCluster
&DBClusterId=pc-xxxxxxxxxxxxxxxxxx
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<DeleteDBClusterResponse>  
	<RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</DeleteDBClusterResponse>
```

JSON格式

```
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

