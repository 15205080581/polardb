# ModifyDBClusterAccessWhiteList {#reference_vrz_3m5_xfb .reference}

该接口用于修改允许访问数据库集群的IP名单。

**说明：** POLARDB for PostgreSQL/Oracle暂不支持该接口。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyDBClusterAccessWhiteList。|
|DBClusterId|String|是|数据库集群ID。|
|SecurityIps|String|是|IP白名单分组下的IP列表，最多1000个，多个IP间用英文逗号（,）隔开，支持如下两种格式： -   IP地址形式，例如：10.23.12.24。
-   CIDR形式，例如：10.23.12.24/24（无类域间路由，24表示了地址中前缀的长度，范围为1~32）。

 |
|DBClusterIPArrayName|String|否|IP白名单分组的名称，不填默认为**Default**分组。 **说明：** 1个集群最多支持50个白名单分组。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|RequestId。|

## 请求示例 {#section_snj_c3s_xfb .section}

``` {#codeblock_8pq_zgk_dbd}
https://polardb.aliyuncs.com/?Action=ModifyDBClusterAccessWhiteList
&DBClusterId=pc-xxxxxxxxx
&SecurityIps=127.0.0.1
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_j2q_tnz_15v}
<ModifyDBClusterAccessWhiteListResponse>  
    <RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</ModifyDBClusterAccessWhiteListResponse>
```

JSON格式

``` {#codeblock_vib_jay_149}
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

