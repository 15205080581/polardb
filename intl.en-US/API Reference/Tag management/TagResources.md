# TagResources {#reference_eyd_tpf_1hb .reference}

You can call this operation to create tags for ApsaraDB for POLARDB clusters.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to TagResources.|
|RegionId|String|Yes|The ID of the region.|
|ResourceType|String|Yes|The type of cluster. Set this parameter to ALIYUN::POLARDB::CLUSTER.|
|ResourceId.n|String|Yes|The ID of the ApsaraDB for POLARDB cluster for which tags are to be created. You can create tags for a maximum of 50 clusters at a time. The number n that follows the ID of each cluster must be different and must be consecutive integers that start from 1. For example, pc-bp1xxx.1 and pc-bp2xxx.2.|
|Tag.n.Key|String|Yes|The key of the tag. You can create up to 20 key-value pairs of tags at a time. The number n in each key-value pair must be different and must be consecutive integers that start from 1. Each value of the Tag.n.Key parameter is paired with a value of the Tag.n.Value parameter.|
|Tag.n.Value|String|Yes|The value of the tag. You can create up to 20 key-value pairs of tags at a time. The number n in each key-value pair must be different and must be consecutive integers that start from 1. Each value of the Tag.n.Value parameter is paired with a value of the Tag.n.Key parameter.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=TagResources
&RegionId=cn-hangzhou
&ResourceId.1=pc-bp15751xxxxxxxx
&ResourceType=ALIYUN%3A%3APOLARDB%3A%3ACLUSTER
&Tag.1.Key=a
&Tag.1.Value=1
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<TagResourcesResponse>
<RequestId>863D51B7-5321-41D8-A0B6-A088B0450EFD</RequestId>
</TagResourcesResponse>
```

JSON format

```

{
"RequestId": "863D51B7-5321-41D8-A0B6-A088B0450EFD"
}
```

