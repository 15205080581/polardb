# DescribeDBClusterAccessWhiteList {#reference_qhl_fn5_xfb .reference}

## 描述 {#section_0t0_kvw_lx5 .section}

该接口用于查看允许访问数据库集群的IP名单。

**说明：** POLARDB for PostgreSQL/Oracle暂不支持该接口。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeDBClusterAccessWhiteList。|
|DBClusterId|String|是|数据库集群ID。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>| |详见[公共返回参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|RequestId。|
|Items|List<DBClusterIPArray\>|集群的IP白名单分组列表。|

## DBClusterIPArray {#section_ilc_b3s_xfb .section}

|参数|类型|描述|
|:-|:-|:-|
|DBClusterIPArrayName|String|IP白名单分组的名称。|
|SecurityIps|String|IP白名单分组下的IP列表，最多1000个，多个IP间用英文逗号（,）隔开，支持如下两种格式： -   IP地址形式，例如：10.23.12.24。
-   CIDR形式，例如：10.23.12.24/24（无类域间路由，24表示了地址中前缀的长度，范围为1~32）。

 |

## 请求示例 {#section_snj_c3s_xfb .section}

``` {#codeblock_862_e09_985}
https://polardb.aliyuncs.com/?Action=DescribeDBClusterAccessWhiteList
&DBClusterId=pc-xxxxxxxxxxx
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_zib_gce_d9d}
<DescribeDBClusterAccessWhiteListResponse>  
    <Items>
        <DBClusterIPArray>
            <DBClusterIPArrayAttribute></DBClusterIPArrayAttribute>
            <DBClusterIPArrayName>default</DBClusterIPArrayName>
            <SecurityIPList>127.0.0.1</SecurityIPList>
        </DBClusterIPArray>
        <DBClusterIPArray>
            <DBClusterIPArrayAttribute>hidden</DBClusterIPArrayAttribute>
            <DBClusterIPArrayName>maxscale</DBClusterIPArrayName>
            <SecurityIPList>11.xx.xx.xx,11.xx.xx.xx</SecurityIPList>
        </DBClusterIPArray>
    </Items>
    <RequestId>8D0429EC-8E2C-4675-8102-28AC6FE92751</RequestId>
</DescribeDBClusterAccessWhiteListResponse>
```

JSON格式

``` {#codeblock_s0i_tfs_lm6}
{
    "Items":{
        "DBClusterIPArray":[
            {
                "DBClusterIPArrayAttribute":"",
                "DBClusterIPArrayName":"default",
                "SecurityIPList":"127.0.0.1"
            },
            {
                "DBClusterIPArrayAttribute":"hidden",
                "DBClusterIPArrayName":"maxscale",
                "SecurityIPList":"11.xx.xx.xx,11.xx.xx.201"
            }
        ]
    },
    "RequestId":"8D0429EC-8E2C-4675-8102-28AC6FE92751"
}
```

