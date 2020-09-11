# DescribeDBClusterAttribute

调用DescribeDBClusterAttribute接口查看PolarDB集群的详细属性。

****

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=polardb&api=DescribeDBClusterAttribute&type=RPC&version=2017-08-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeDBClusterAttribute|系统规定参数，取值为DescribeDBClusterAttribute。 |
|DBClusterId|String|是|pc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|集群ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Category|String|Normal|集群系列，取值范围如下：

 -   **Normal**：标准版
-   **Basic**：普惠版 |
|CreationTime|String|2020-03-23T05:35:43Z|集群创建时间。 |
|DBClusterDescription|String|GDN测试|集群描述。 |
|DBClusterId|String|pc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|集群ID。 |
|DBClusterNetworkType|String|VPC|集群的网络类型。 |
|DBClusterStatus|String|Running|集群状态，取值范围如下：

 -   Creating：创建中
-   Running：运行中
-   Deleting：释放中
-   Rebooting：重启中
-   DBNodeCreating：正在增加节点
-   DBNodeDeleting：正在删除节点
-   ClassChanging：正在变更节点规格
-   NetAddressCreating：正在创建网络连接
-   NetAddressDeleting：正在删除网络连接
-   NetAddressModifying：正在修改网络连接
-   Deleted：已释放 |
|DBNodes|Array of DBNode| |DBNode组成的集合。 |
|CreationTime|String|2020-03-23T21:35:43Z|节点创建时间。 |
|DBNodeClass|String|polar.mysql.x4.large|节点规格。 |
|DBNodeId|String|pi-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|节点ID。 |
|DBNodeRole|String|Reader|节点角色，取值范围如下：

 -   Writer：主节点。
-   Reader：只读节点。 |
|DBNodeStatus|String|Running|节点状态，取值范围如下：

 -   Creating：创建中
-   Running：运行中
-   Deleting：删除中
-   Rebooting：重启中
-   DBNodeCreating：正在增加节点
-   DBNodeDeleting：正在删除节点
-   ClassChanging：正在变更节点规格
-   NetAddressCreating：正在创建网络连接
-   NetAddressDeleting：正在删除网络连接
-   NetAddressModifying：正在修改网络连接
-   MinorVersionUpgrading：小版本升级中
-   Maintaining：实例维护中
-   Switching：切换中 |
|FailoverPriority|Integer|1|Failover优先级。每个节点都有一个Failover优先级，决定了当故障切换时，该节点被选举为主节点的概率高低。数值越大，优先级越高，取值范围为1~15。 |
|MaxConnections|Integer|1200|最大集群并发连接数。 |
|MaxIOPS|Integer|8000|最大I/O请求次数，即IOPS。 |
|ZoneId|String|cn-qingdao-c|可用区ID。 |
|DBType|String|MySQL|数据库引擎类型。 |
|DBVersion|String|8.0|数据库引擎版本。 |
|DataLevel1BackupChainSize|Long|1389363200|一级备份（快照）总大小，单位为Byte。 |
|DeletionLock|Integer|0|集群删除的锁定状态：

 -   0：未锁定，可删除集群。
-   1：锁定，不可删除集群。 |
|Engine|String|POLARDB|集群引擎。 |
|ExpireTime|String|2020-06-14T16:00:00Z|到期时间。

 **说明：** 按量付费集群无到期时间。 |
|Expired|String|false|是否过期。 |
|IsLatestVersion|Boolean|false|是否为最新内核版本。 |
|LockMode|String|Unlock|锁定模式，取值范围如下：

 -   Unlock：未锁定。
-   ManualLock：手动触发锁定。
-   LockByExpiration：集群过期自动锁定。 |
|MaintainTime|String|16:00Z-17:00Z|集群的可维护时间段（UTC时间），格式为`HH:mmZ-HH:mmZ`。例如`16:00Z-17:00Z`表示，0点到1点（UTC+08:00）可以进行例行维护。 |
|PayType|String|Postpaid|付费类型：

 -   Postpaid：按量付费。
-   Prepaid：预付费（包年包月）。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|RequestId|String|6A8952B9-6ADD-4AF6-A96F-6C01B6\*\*\*\*\*\*|请求ID。 |
|ResourceGroupId|String|rg-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|资源组ID。 |
|SQLSize|Long|0|SQL的存储量，单位为Byte。若数值为-1，则表示没有数据。 |
|StorageMax|Long|10995116277760|当前集群规格的最大存储容量，单位为Byte。 |
|StorageUsed|Long|4864344064|存储空间的使用量，单位为Byte。 |
|Tags|Array of Tag| |标签组成的集合。 |
|Key|String|test1|标签键。 |
|Value|String|1111|标签值。 |
|VPCId|String|vpc-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|专有网络ID。 |
|VSwitchId|String|vsw-\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*|虚拟交换机ID。 |
|ZoneIds|String|cn-hangzhou-i|数据分布的可用区。 |

## 示例

请求示例

```
http(s)://polardb.aliyuncs.com/?Action=DescribeDBClusterAttribute
&DBClusterId=pc-*****************
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DeletionLock>0</DeletionLock>
<Category>Normal</Category>
<ResourceGroupId>rg-***************</ResourceGroupId>
<DataLevel1BackupChainSize>1389363200</DataLevel1BackupChainSize>
<DBClusterId>pc-*****************</DBClusterId>
<DBClusterNetworkType>VPC</DBClusterNetworkType>
<DBType>MySQL</DBType>
<IsLatestVersion>false</IsLatestVersion>
<DBVersion>8.0</DBVersion>
<StorageMax>10995116277760</StorageMax>
<DBNodes>
    <DBNodeStatus>Running</DBNodeStatus>
    <ZoneId>cn-hangzhou-i</ZoneId>
    <MaxConnections>8000</MaxConnections>
    <DBNodeRole>Reader</DBNodeRole>
    <CreationTime>2020-03-23T21:35:43Z</CreationTime>
    <DBNodeId>pi-****************</DBNodeId>
    <FailoverPriority>1</FailoverPriority>
    <DBNodeClass>polar.mysql.x4.large</DBNodeClass>
    <MaxIOPS>32000</MaxIOPS>
</DBNodes>
<DBNodes>
    <DBNodeStatus>Running</DBNodeStatus>
    <ZoneId>cn-hangzhou-i</ZoneId>
    <MaxConnections>8000</MaxConnections>
    <DBNodeRole>Writer</DBNodeRole>
    <CreationTime>2020-03-23T21:35:43Z</CreationTime>
    <DBNodeId>pi-****************</DBNodeId>
    <FailoverPriority>0</FailoverPriority>
    <DBNodeClass>polar.mysql.x4.large</DBNodeClass>
    <MaxIOPS>32000</MaxIOPS>
</DBNodes>
<DBNodes>
    <DBNodeStatus>Running</DBNodeStatus>
    <ZoneId>cn-hangzhou-i</ZoneId>
    <MaxConnections>8000</MaxConnections>
    <DBNodeRole>Reader</DBNodeRole>
    <CreationTime>2020-05-08T18:28:22Z</CreationTime>
    <DBNodeId>pi-****************</DBNodeId>
    <FailoverPriority>1</FailoverPriority>
    <DBNodeClass>polar.mysql.x4.large</DBNodeClass>
    <MaxIOPS>32000</MaxIOPS>
</DBNodes>
<ZoneIds>cn-hangzhou-i,cn-hangzhou-i</ZoneIds>
<MaintainTime>16:00Z-17:00Z</MaintainTime>
<Engine>POLARDB</Engine>
<RequestId>6A8952B9-6ADD-4AF6-A96F-6C01B6******</RequestId>
<VPCId>vpc-*******************</VPCId>
<DBClusterStatus>Running</DBClusterStatus>
<VSwitchId>vsw-*********************</VSwitchId>
<DBClusterDescription>GDN测试</DBClusterDescription>
<Expired>false</Expired>
<PayType>Postpaid</PayType>
<LockMode>Unlock</LockMode>
<StorageUsed>4864344064</StorageUsed>
<CreationTime>2020-03-23T05:35:43Z</CreationTime>
<RegionId>cn-hangzhou</RegionId>
<SQLSize>0</SQLSize>
<ExpireTime/>
```

`JSON` 格式

```
{
	"DeletionLock": 0,
    "Category": "Normal",
	"ResourceGroupId": "rg-***************",
	"DataLevel1BackupChainSize": 1389363200,
	"DBClusterId": "pc-*****************",
	"DBClusterNetworkType": "VPC",
	"DBType": "MySQL",
	"IsLatestVersion": false,
	"DBVersion": "8.0",
	"StorageMax": 10995116277760,
	"DBNodes": [
		{
			"DBNodeStatus": "Running",
			"ZoneId": "cn-hangzhou-i",
			"MaxConnections": 8000,
			"DBNodeRole": "Reader",
			"CreationTime": "2020-03-23T21:35:43Z",
			"DBNodeId": "pi-****************",
			"FailoverPriority": 1,
			"DBNodeClass": "polar.mysql.x4.large",
			"MaxIOPS": 32000
		},
		{
			"DBNodeStatus": "Running",
			"ZoneId": "cn-hangzhou-i",
			"MaxConnections": 8000,
			"DBNodeRole": "Writer",
			"CreationTime": "2020-03-23T21:35:43Z",
			"DBNodeId": "pi-****************",
			"FailoverPriority": 0,
			"DBNodeClass": "polar.mysql.x4.large",
			"MaxIOPS": 32000
		},
		{
			"DBNodeStatus": "Running",
			"ZoneId": "cn-hangzhou-i",
			"MaxConnections": 8000,
			"DBNodeRole": "Reader",
			"CreationTime": "2020-05-08T18:28:22Z",
			"DBNodeId": "pi-****************",
			"FailoverPriority": 1,
			"DBNodeClass": "polar.mysql.x4.large",
			"MaxIOPS": 32000
		}
	],
	"ZoneIds": "cn-hangzhou-i,cn-hangzhou-i",
	"MaintainTime": "16:00Z-17:00Z",
	"Engine": "POLARDB",
	"Tags": [],
	"RequestId": "6A8952B9-6ADD-4AF6-A96F-6C01B6******",
	"VPCId": "vpc-*******************",
	"DBClusterStatus": "Running",
	"VSwitchId": "vsw-*********************",
	"DBClusterDescription": "GDN测试",
	"Expired": false,
	"PayType": "Postpaid",
	"LockMode": "Unlock",
	"StorageUsed": 4864344064,
	"CreationTime": "2020-03-23T05:35:43Z",
	"RegionId": "cn-hangzhou",
	"SQLSize": 0,
	"ExpireTime": ""
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/polardb)查看更多错误码。

