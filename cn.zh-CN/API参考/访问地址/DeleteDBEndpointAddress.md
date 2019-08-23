# DeleteDBEndpointAddress {#reference_wzw_12z_xfb .reference}

该接口用于释放POLARDB集群公网地址。

**说明：** 释放POLARDB自定义集群地址请参见[DeleteDBClusterEndpoint](intl.zh-CN/API参考/访问地址/DeleteDBClusterEndpoint.md#)。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DeleteDBEndpointAddress。|
|DBClusterId|String|是|集群ID。|
|EndpointId|String|是|集群地址ID。例如pe-xxxxxxxx。|
|NetType|String|是|IP 网络类型，取值：Public。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|RequestId|

## 请求示例 {#section_khc_1dz_xfb .section}

``` {#codeblock_j28_loq_21j}
https://polardb.aliyuncs.com/?Action=DeleteDBEndpointAddress
&DBClusterId=pc-xxxxxxxxxx
&DBEndpointId=pe-xxxxxxxxxx
&NetType=Public
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_jiq_fcc_3jr}
<DeleteDBEndpointAddressResponse>  
    <RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</DeleteDBEndpointAddressResponse>
```

JSON格式

``` {#codeblock_9bj_7n2_5lf}
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

