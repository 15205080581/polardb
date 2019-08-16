# CreateDBNodes {#reference_zpr_187230 .reference}

该接口用于增加POLARDB集群节点。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：CreateDBNodes。|
|DBClusterId|String|是|集群ID。|
|DBNode.N.ZoneId|String|否|新增节点的可用区，需要与原有节点保持一致。N为从1开始的整数，最大值=16-当前节点数。DBNode.N.ZoneId和DBNode.N.TargetClass，至少填一个。可用区ID可以通过接口[DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#)查询。 **说明：** 当前暂不支持一次增加多个节点。

 |
|DBNode.N.TargetClass|String|否|新增节点的规格，需要与原有节点保持一致。N为从1开始的整数，最大值=16-当前节点数。DBNode.N.ZoneId和DBNode.N.TargetClass，至少填一个。规格详情请参见[../../../../dita-oss-bucket/SP\_61/DNPOLA1875676/ZH-CN\_TP\_3012\_V32.md\#](../../../../intl.zh-CN/产品定价/规格与定价.md#)。 **说明：** 当前暂不支持一次增加多个节点。

 |
|ClientToken|String|否|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，保证在不同请求间唯一，大小写敏感、不超过64个ASCII字符。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|RequestId。|
|DBClusterId|String|数据库集群ID。|
|OrderId|String|订单ID。|

## 请求示例 {#section_khc_1dz_xfb .section}

```
https://polardb.aliyuncs.com/?Action=CreateDBNodes
&DBClusterId=pc-xxxxxxxxxx
&DBNode.N.TargetClass=polar.mysql.x2.medium
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<CreateDBNodesResponse>  
	<OrderId>2035624xxxxxxxx</OrderId>
	<RequestId>C5BC3F8D-37C0-40EF-B5EF-457F983C612A</RequestId>
	<DBClusterId>pc-xxxxxxxxxxxxx</DBClusterId>
</CreateDBNodesResponse>
```

JSON格式

```
{
	"OrderId": 2035624xxxxxxxx,
	"RequestId": "C5BC3F8D-37C0-40EF-B5EF-457F983C612A",
	"DBClusterId": "pc-xxxxxxxxxxxxx"
}
```

