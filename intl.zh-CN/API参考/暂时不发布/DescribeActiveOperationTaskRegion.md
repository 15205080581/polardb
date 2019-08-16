# DescribeActiveOperationTaskRegion {#reference_d2m_mkz_xfb .reference}

获取任务region与各类型任务数。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|说明|
|:-|:-|:---|:-|
|Action|String|是|DescribeActiveOperationTaskRegion|
|IsHistory|Integer|否|是否返回历史任务, 0表示返回当前任务, 1表示返回历史任务, 默认0|
|TaskType|String|是|任务类型|
|ProductName|String|是|产品名称, RDS/MongoDB/Redis/POLARDB|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|说明|
|:-|:-|:-|
|RegionList|List<Item\>|region列表, 数据格式：\{item,item2,item3, ...\}|

## Item参数 {#section_ens_mmz_xfb .section}

|参数|类型|说明|
|:-|:-|:-|
|Region|String|可用区|
|Count|Integer|待处理任务数|

## 错误信息 {#section_khc_1dz_xfb .section}

|Error|Description|HTTP Status Code|
|:----|:----------|:---------------|
|RequiredParam.NotFound|Required input param is not found.|400|

