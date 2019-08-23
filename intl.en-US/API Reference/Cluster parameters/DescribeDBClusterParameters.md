# DescribeDBClusterParameters {#reference_j3j_jgt_xfb .reference}

You can call this operation to query the parameters of a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeDBClusterParameters.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to be queried.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|
|Engine|String|The engine of the cluster.|
|RunningParameters|List<Parameter\>|The list of running parameters of the cluster.|

## Parameter {#section_ilc_b3s_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|ParameterName|String|The name of the parameter.|
|ParameterValue|String|The value of the parameter.|
|ParameterDescription|String|The description of the parameter.|
|DataType|String|The value type of the parameter.|
|DefaultParameterValue|String|The default value of the parameter.|
|IsModifiable|String|Indicates whether the parameter can be modified. Valid values: -   false: The parameter cannot be modified.
-   true: The parameter can be modified.

 |
|ForceRestart|String|Indicates whether a cluster restart is required to make the modified value of the parameter take effect. Valid values: -   false: A cluster restart is not required.
-   true: A cluster restart is required.

 |
|ParameterStatus|String|The status of the parameter. Valid values: -   normal: The parameter is normal.
-   modifying: The parameter is being modified.

 |
|CheckingCode|String|The verification code of the parameter, which indicates the valid values of the parameter.|

## Sample request {#section_khc_1dz_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeDBClusterParameters
&DBClusterId=pc-xxxxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<DescribeDBClusterParametersResponse>  
	<RequestId>0FF7F658-ECE2-476C-B3C5-122BA9EB43C6</RequestId>
	<RunningParameters>
		<Parameter />
	</RunningParameters>
	<Engine>POLARDB</Engine>
</DescribeDBClusterParametersResponse>
```

JSON format

```
{
    "RequestId":"0FF7F658-ECE2-476C-B3C5-122BA9EB43C6",
    "RunningParameters":{
        "Parameter":Array[176]
    },
    "Engine":"POLARDB"
}
```

