# DescribeDBClusterParameters {#reference_j3j_jgt_xfb .reference}

该接口用于查看POLARDB集群的参数。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeDBClusterParameters。|
|DBClusterId|String|是|集群ID。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|RequestId。|
|Engine|String|引擎。|
|RunningParameters|List<Parameter\>|当前运行的参数列表。|

## Parameter {#section_ilc_b3s_xfb .section}

|参数|类型|描述|
|:-|:-|:-|
|ParameterName|String|参数名。|
|ParameterValue|String|参数值。|
|ParameterDescription|String|参数描述。|
|DataType|String|值类型。|
|DefaultParameterValue|String|参数默认值。|
|IsModifiable|String|是否可修改： -   False：不可修改；
-   True：可修改。

 |
|ForceRestart|String|是否需要重启生效： -   False：否；
-   True：是。

 |
|ParameterStatus|String|参数状态： -   normal：正常；
-   modifying：修改中。

 |
|CheckingCode|String|校验代码，参数的可选范围。|

## 请求示例 {#section_khc_1dz_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeDBClusterParameters
&DBClusterId=pc-xxxxxxxxxx
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<DescribeDBClusterParametersResponse>  
	<RequestId>0FF7F658-ECE2-476C-B3C5-122BA9EB43C6</RequestId>
	<RunningParameters>
		<Parameter />
	</RunningParameters>
	<Engine>POLARDB</Engine>
</DescribeDBClusterParametersResponse>
```

JSON格式

```
{
    "RequestId":"0FF7F658-ECE2-476C-B3C5-122BA9EB43C6",
    "RunningParameters":{
        "Parameter":Array[176]
    },
    "Engine":"POLARDB"
}
```

