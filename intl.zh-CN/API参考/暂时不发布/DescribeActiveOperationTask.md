# DescribeActiveOperationTask {#reference_txp_zmz_xfb .reference}

用户侧查询运维任务。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|说明|
|:-|:-|:---|:-|
|Action|String|是|DescribeActiveOperationTask|
|PageSize|Integer|否|每页记录数, 默认每页25条|
|PageNumber|Integer|否|页码，大于0, 默认1|
|IsHistory|Integer|否|是否返回历史任务, 0表示返回当前任务, 1表示返回历史任务, 默认0|
|TaskType|String|是|任务类型|
|Region|String|是|可用区|
|ProductName|String|是|产品名称, RDS/MongoDB/Redis/POLARDB|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|说明|
|:-|:-|:-|
|PageSize|Integer|每页记录数|
|PageNumber|Integer|页码|
|TotalRecordCount|Integer|总记录数|
|Items|List<Item\>|记录列表, 数据格式：\{item,item2,item3, ...\}|

## Item参数 {#section_ens_mmz_xfb .section}

|参数|类型|说明|
|:-|:-|:-|
|Id|Integer|任务id, 可以传多个, 用逗号分隔|
|InsName|String|实例名|
|StartTime|String|后台执行任务的时间点, 格式为YYYY-MM-DD HH:mm:ss，如2018-05-30 00:00:00|
|SwitchTime|String|后台发起切换操作的时间点, 格式为YYYY-MM-DD HH:mm:ss，如2018-05-30 14:30:00|
|Deadline|String|任务执行时间可调整范围的最晚期限, 格式为YYYY-MM-DD HH:mm:ss，如2018-05-30 23:59:59|
|Status|Integer|任务状态待处理页面: 2表示等待用户指定时间3表示等待处理4表示处理中\(此状态不可更改时间\)历史页面:5表示成功结束6表示失败结束7已取消|
|CreatedTime|String|创建时间, 格式为YYYY-MM-DD HH:mm:ss，如2018-05-30 14:30:00|
|ModifiedTime|String|修改时间, 格式为YYYY-MM-DD HH:mm:ss，如2018-05-30 14:30:00|
|ResultInfo|String|执行结果信息|
|PrepareInterval|String|开始时间到切换时间之间所需的准备时间, 格式为HH:mm:ss，如04:00:00|
|TaskParams|String|任务参数|
|TaskType|String|任务类型|
|DbType|String|数据库类型|

## 错误信息 {#section_khc_1dz_xfb .section}

|Error|Description|HTTP Status Code|
|:----|:----------|:---------------|
|InvalidPageParam.Format|Page param should be a positive integer.|400|
|RequiredParam.NotFound|Required input param is not found.|400|

