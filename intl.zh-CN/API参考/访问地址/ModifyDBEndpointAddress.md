# ModifyDBEndpointAddress {#reference_rwk_tdz_xfb .reference}

该接口用于修改POLARDB集群默认访问地址前缀。

**说明：** POLARDB for PostgreSQL/Oracle暂不支持该接口。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyDBEndpointAddress。|
|DBClusterId|String|是|集群ID。|
|EndpointId|String|是|集群地址ID。例如pe-xxxxxxxx。|
|NetType|String|是|IP 网络类型： -   Public（公网）；
-   Private（私网）。

 |
|ConnectionStringPrefix|String|否|新的连接地址前缀： -   不能以中划线结尾；
-   由小写字母，数字，中划线组成，字母开头；
-   长度大于6个字符。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|RequestId。|

## 请求示例 {#section_khc_1dz_xfb .section}

``` {#codeblock_h4m_o5g_h9w}
https://polardb.aliyuncs.com/?Action=ModifyDBEndpointAddress
&DBClusterId=pc-xxxxxxxxxx
&DBEndpointId=pe-xxxxxxxxxx
&ConnectionStringPrefix=pc-xxxxxxxxxx-pub2
&NetType=Public
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_mv7_to0_28x}
<CreateDBEndpointAddressResponse>  
    <RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</CreateDBEndpointAddressResponse>
```

JSON格式

``` {#codeblock_kax_luv_jcv}
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

