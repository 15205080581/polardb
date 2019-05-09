# DescribeDBClusterAttribute {#reference_p5z_535_xfb .reference}

该接口用于查看指定POLARDB集群的详细属性。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeDBClusterAttribute。|
|DBClusterId|String|是|集群ID。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RegionId|String|地域ID。|
|DBClusterId|String|集群ID。|
|DBClusterDescription|String|集群描述。|
|PayType|String|付费类型： -   Postpaid：按量付费；
-   Prepaid：预付费（包年包月）。

 |
|Engine|String|集群引擎。|
|DBType|String|数据库类型。|
|DBVersion|String|数据库版本。|
|DBClusterStatus|String|集群状态，详见[集群状态表](cn.zh-CN/API参考/附表/集群状态表.md#)。|
|LockMode|String|锁定模式： -   Unlock：正常；
-   ManualLock：手动触发锁定；
-   LockByExpiration：集群过期自动锁定。

 |
|DBClusterNetworkType|String|集群的网络类型。|
|VPCId|String|专有网络ID。|
|VSwitchId|String|虚拟交换机ID。|
|StorageUsed|Long|存储用量，单位：Byte。|
|CreationTime|String|创建时间，格式：*YYYY-MM-DD*T*hh:mm:ss*Z，如2011-05-30T12:11:4Z。|
|ExpireTime|String|到期时间。 **说明：** 按量付费集群无到期时间。

 |
|MaintainTime|String|集群的可维护时间： 格式：*HH:mm*Z-*HH:mm*Z

 示例：16:00Z-17:00Z，表示0点到1点\(UTC+08:00\)可进行例行维护。

 |
|DBNodes|List<DBNode\>|DBNode组成的集合。|
|Tags|List<Tag\>|Tag组成的集合。|

## DBNode参数 {#section_lmx_xg5_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|DBNodeId|String|节点ID。|
|ZoneId|String|可用区ID。|
|DBInstanceStatus|String|节点状态。|
|CreationTime|String|创建时间。|
|DBNodeClass|String|节点规格。|
|DBNodeRole|String|节点角色： -   Writer；
-   Reader。

 |
|MaxIOPS|Integer|最大IO请求次数，即IOPS。|
|MaxConnections|Integer|最大集群并发连接数。|

## Tag参数 {#section_yth_nv1_1hb .section}

|名称|类型|描述|
|:-|:-|:-|
|Key|String|标签键。|
|Value|String|标签值。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeDBClusterAttribute
&DBClusterId=pc-xxxxxxxxxxxxxxx
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<DescribeDBClusterAttributeResponse>  
	<DBVersion>5.6</DBVersion>
	<LockMode>Unlock</LockMode>
	<DBClusterDescription>test</DBClusterDescription>
	<DBClusterNetworkType>VPC</DBClusterNetworkType>
	<DBClusterId>pc-xxxxxxxxxxxxxx</DBClusterId>
	<VSwitchId>vsw-xxxxxxxxxxxxxx</VSwitchId>
	<Engine>POLARDB</Engine>
	<DBClusterStatus>Running</DBClusterStatus>
	<CreationTime>2019-04-26T06:01:28Z</CreationTime>
	<MaintainTime>18:00Z-19:00Z</MaintainTime>
	<VPCId>vpc-xxxxxxxxxxxxxx</VPCId>
	<ExpireTime></ExpireTime>
	<Expired>false</Expired>
	<RequestId>4E148395-950A-46F8-BFF8-274A64CD793B</RequestId>
	<RegionId>cn-qingdao</RegionId>
	<DBType>MySQL</DBType>
	<DBNodes>
		<CreationTime>2019-04-26T22:01:28Z</CreationTime>
		<MaxIOPS>8000</MaxIOPS>
		<DBNodeRole>Writer</DBNodeRole>
		<MaxConnections>1200</MaxConnections>
		<DBNodeClass>polar.mysql.x2.medium</DBNodeClass>
		<DBNodeStatus>Running</DBNodeStatus>
		<ZoneId>cn-qingdao-c</ZoneId>
		<DBNodeId>pi-xxxxxxxxxxxxxx</DBNodeId>
	</DBNodes>
	<DBNodes>
		<CreationTime>2019-04-26T22:01:28Z</CreationTime>
		<MaxIOPS>8000</MaxIOPS>
		<DBNodeRole>Reader</DBNodeRole>
		<MaxConnections>1200</MaxConnections>
		<DBNodeClass>polar.mysql.x2.medium</DBNodeClass>
		<DBNodeStatus>Running</DBNodeStatus>
		<ZoneId>cn-qingdao-c</ZoneId>
		<DBNodeId>pi-xxxxxxxxxxxxxx</DBNodeId>
	</DBNodes>
	<SQLSize>0</SQLSize>
	<PayType>Postpaid</PayType>
</DescribeDBClusterAttributeResponse>
```

JSON格式

```
{
	"DBVersion": "5.6",
	"LockMode": "Unlock",
	"DBClusterDescription": "test",
	"DBClusterNetworkType": "VPC",
	"DBClusterId": "pc-xxxxxxxxxxxxxx",
	"VSwitchId": "vsw-xxxxxxxxxxxxxx",
	"Engine": "POLARDB",
	"DBClusterStatus": "Running",
	"CreationTime": "2019-04-26T06:01:28Z",
	"MaintainTime": "18:00Z-19:00Z",
	"Tags": [],
	"VPCId": "vpc-xxxxxxxxxxxxxx",
	"ExpireTime": "",
	"Expired": false,
	"RequestId": "4E148395-950A-46F8-BFF8-274A64CD793B",
	"RegionId": "cn-qingdao",
	"DBType": "MySQL",
	"DBNodes": [
		{
			"CreationTime": "2019-04-26T22:01:28Z",
			"MaxIOPS": 8000,
			"DBNodeRole": "Writer",
			"MaxConnections": 1200,
			"DBNodeClass": "polar.mysql.x2.medium",
			"DBNodeStatus": "Running",
			"ZoneId": "cn-qingdao-c",
			"DBNodeId": "pi-xxxxxxxxxxxxxx"
		},
		{
			"CreationTime": "2019-04-26T22:01:28Z",
			"MaxIOPS": 8000,
			"DBNodeRole": "Reader",
			"MaxConnections": 1200,
			"DBNodeClass": "polar.mysql.x2.medium",
			"DBNodeStatus": "Running",
			"ZoneId": "cn-qingdao-c",
			"DBNodeId": "pi-xxxxxxxxxxxxxx"
		}
	],
	"SQLSize": 0,
	"PayType": "Postpaid"
}
```

