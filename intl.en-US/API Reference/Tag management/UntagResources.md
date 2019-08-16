# UntagResources {#reference_k5d_gsf_1hb .reference}

You can call this operation to delete tags for ApsaraDB for POLARDB clusters.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to UntagResources.|
|RegionId|String|Yes|The ID of the region.|
|ResourceType|String|Yes|The type of cluster. Set this parameter to ALIYUN::POLARDB::CLUSTER.|
|ResourceId.n|String|Yes|The ID of the ApsaraDB for POLARDB cluster for which tags are to be deleted. You can delete tags for a maximum of 50 clusters at a time. The number n that follows the ID of each cluster must be different and must be consecutive integers that start from 1. For example, pc-bp1xxx.1 and pc-bp2xxx.2.|
|TagKey.n|String|No|The key of the tag. You can delete up to 20 key-value pairs of tags at a time. The number n in each key-value pair must be different and must be consecutive integers that start from 1.|
|All|String|No|Specifies whether to delete all tags. This parameter takes effect only when the TagKey.n parameter is not specified. Valid values: -   true
-   false

 Default value: false.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=UntagResources
&RegionId=cn-hangzhou
&ResourceId.1=pc-bp15751xxxxxxxx
&ResourceType=ALIYUN%3A%3APOLARDB%3A%3ACLUSTER
&&TagKey.1=a
&<[Common request parameters]>
				
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<UntagResourcesResponse>
    <RequestId>2D69A58F-345C-4FDE-88E4-BF5189484043</RequestId>
</UntagResourcesResponse>
```

JSON format

```
{ 
"RequestId": "2D69A58F-345C-4FDE-88E4-BF5189484043", 
}
```

