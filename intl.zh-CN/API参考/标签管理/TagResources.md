# TagResources {#reference_eyd_tpf_1hb .reference}

该接口用于为POLARDB集群创建标签。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：TagResources。|
|RegionId|String|是|地域ID。|
|ResourceType|String|是|集群类型，取值：ALIYUN::POLARDB::CLUSTER。|
|ResourceId.n|String|是|第n个需要创建标签的集群ID。每次最多为50个集群同时添加标签，各个集群ID后面的数字n必须不同，且必须是从1开始的连续整数。例如：pc-bp1xxx.1、pc-bp2xxx.2。|
|Tag.n.Key|String|是|标签键。每次最多添加20对标签，各个标签对的数字n必须不同，且必须是从1开始的连续整数。Tag.n.Key对应的值为Tag.n.Vlaue。|
|Tag.n.Value|String|是|标签值。每次最多添加20对标签，各个标签对的数字n必须不同，且必须是从1开始的连续整数。Tag.n.Vlaue是Tag.n.Key的值。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|RequestId。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=TagResources
&RegionId=cn-hangzhou
&ResourceId.1=pc-bp15751xxxxxxxx
&ResourceType=ALIYUN%3A%3APOLARDB%3A%3ACLUSTER
&Tag.1.Key=a
&Tag.1.Value=1
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<TagResourcesResponse>
<RequestId>863D51B7-5321-41D8-A0B6-A088B0450EFD</RequestId>
</TagResourcesResponse>
```

JSON格式

```

{
"RequestId": "863D51B7-5321-41D8-A0B6-A088B0450EFD"
}
```

