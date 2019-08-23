# DescribeDBClusterNetInfo {#reference_gkh_gcz_xab .reference}

该接口用于查询POLARDB集群的网络信息。

**说明：** 暂不发布，下线。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeDBClusterNetInfo。|
|DBClusterId|String|是|数据库集群ID。|
|ConnectionStringType|String|否|查询连接串类型： -   Normal：普通连接；
-   ReadWriteSplitting：读写分离连接；
-   MPP：MPP连接。

 不传则返回所有连接。

 |

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|RequestId。|
|ClusterNetworkType|String|集群的网络类型。|
|ConnectionString|String|集群访问地址。|
|IPAddress|String|IP地址。|
|IPType|String|IP地址类型： -   公网：Public；
-   内网VPC：Private；
-   内网经典网络：Inner。

 |
|Port|String|端口|
|VPCId|String|专有网络ID。|
|VSwitchId|String|虚拟交换机ID。|
|ConnectionStringType|String|查询连接串类型： -   Normal：普通连接；
-   ReadWriteSplitting：读写分离连接；
-   MPP：MPP连接。

 |

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeDBClusterNetInfo
&DBClusterId=pc-xxxxxxxxxx
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<DescribeDBClusterEndpointsResponse>  
	<Items>
		<EndpointType>Primary</EndpointType>
		<Nodes>Auto</Nodes>
		<DBEndpointId>pc-xxxxxxxxxx</DBEndpointId>
		<NetInfoItems>
			<Port>3306</Port>
			<ConnectionString>pe-xxxxxxxxxx.w.polardb.cn-qd-pldb1.rds.aliyuncs.com</ConnectionString>
			<VPCId>vpc-xxxxxxxxxx</VPCId>
			<IPAddress>172.xx.xx.xx</IPAddress>
			<NetType>Private</NetType>
			<VSwitchId>vsw-xxxxxxxxxx</VSwitchId>
		</NetInfoItems>
		<NetInfoItems>
			<Port>3306</Port>
			<ConnectionString>pe-xxxxxxxxxx.w.polardb.cn-qd-pldb1.rds.aliyuncs.com</ConnectionString>
			<VPCId></VPCId>
			<IPAddress>120.xx.xx.xx</IPAddress>
			<NetType>Public</NetType>
			<VSwitchId></VSwitchId>
		</NetInfoItems>
		<EndpointConfig>null</EndpointConfig>
	</Items>
	<Items>
		<EndpointType>Cluster</EndpointType>
		<Nodes>Auto</Nodes>
		<DBEndpointId>pe-xxxxxxxxxx</DBEndpointId>
		<NetInfoItems>
			<Port>3306</Port>
			<ConnectionString>pe-xxxxxxxxxx.polardb.cn-qd-pldb1.rds.aliyuncs.com</ConnectionString>
			<VPCId>vpc-xxxxxxxxxx</VPCId>
			<IPAddress>172.xx.xx.xx</IPAddress>
			<NetType>Private</NetType>
			<VSwitchId>vsw-xxxxxxxxxx</VSwitchId>
		</NetInfoItems>
		<EndpointConfig>{&quot;CausalConsistRead&quot;:0,&quot;WriterAcceptReads&quot;:0,&quot;LoadBalanceStrategy&quot;:&quot;load&quot;}</EndpointConfig>
	</Items>
	<RequestId>3FAC22CA-AADE-40A2-9841-30BDC81C4E9C</RequestId>
</DescribeDBClusterEndpointsResponse>
```

JSON格式

```
{
    "Items":[
        {
            "EndpointType":"Primary",
            "Nodes":"Auto",
            "DBEndpointId":"pc-xxxxxxxxxx",
            "NetInfoItems":[
                {
                    "Port":"3306",
                    "ConnectionString":"pe-xxxxxxxxxx.w.polardb.cn-qd-pldb1.rds.aliyuncs.com",
                    "VPCId":"vpc-xxxxxxxxxx",
                    "IPAddress":"172.xx.xx.xx",
                    "NetType":"Private",
                    "VSwitchId":"vsw-xxxxxxxxxx"
                },
                {
                    "Port":"3306",
                    "ConnectionString":"pe-xxxxxxxxxx.w.polardb.cn-qd-pldb1.rds.aliyuncs.com",
                    "VPCId":"",
                    "IPAddress":"120.xx.xx.xx",
                    "NetType":"Public",
                    "VSwitchId":""
                }
            ],
            "EndpointConfig":"null"
        },
        {
            "EndpointType":"Cluster",
            "Nodes":"Auto",
            "DBEndpointId":"pe-xxxxxxxxxx",
            "NetInfoItems":[
                {
                    "Port":"3306",
                    "ConnectionString":"pe-xxxxxxxxxx.polardb.cn-qd-pldb1.rds.aliyuncs.com",
                    "VPCId":"vpc-xxxxxxxxxx",
                    "IPAddress":"172.xx.xx.xx",
                    "NetType":"Private",
                    "VSwitchId":"vsw-xxxxxxxxxx"
                }
            ],
            "EndpointConfig":"{"CausalConsistRead":0,"WriterAcceptReads":0,"LoadBalanceStrategy":"load"}"
        }
    ],
    "RequestId":"3FAC22CA-AADE-40A2-9841-30BDC81C4E9C"
}
```

