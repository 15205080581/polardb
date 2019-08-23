# ModifyActiveOperationTask {#reference_efw_lnz_xfb .reference}

用户侧修改任务。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|说明|
|:-|:-|:---|:-|
|Action|String|是|ModifyActiveOperationTask|
|Ids|String|是|批量修改id列表|
|SwitchTime|String|是|后台发起切换操作的时间点, 格式为YYYY-MM-DD HH:mm:ss，如2018-05-30 14:30:00|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|说明|
|:-|:-|:-|
|Ids|String|批量修改id列表|

## 错误信息 {#section_khc_1dz_xfb .section}

|Error|Description|HTTP Status Code|
|:----|:----------|:---------------|
|RequiredParam.NotFound|Required input param is not found.|400|
|InvalidTime.Format|Specified time is not valid.|400|
|TaskModifyError|Part of the tasks cannot be modified.|400|
|ParameterLeastAssociate|Must input at least one optional parameter.|403|
|SwitchTimeAfterDeadline|The switch time should be earlier than deadline.|400|

