# DescribeActiveOperationTaskCount {#reference_ntg_zfz_xfb .reference}

该接口用于获取运维任务数与是否弹窗。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|说明|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeActiveOperationTaskCount。|
|ProductName|String|是|产品名称，POLARDB|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|说明|
|:-|:-|:-|
|TaskCount|Integer|待处理任务数。|
|NeedPop|Integer|是否需要弹窗通知用户，0表示不需要弹窗, 1表示需要弹窗。|

## 错误信息 {#section_khc_1dz_xfb .section}

|Error|Description|HTTP Status Code|
|:----|:----------|:---------------|
|RequiredParam.NotFound|Required input param is not found.|400|

