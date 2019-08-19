# ModifyDBClusterParameters {#reference_zst_xgt_xfb .reference}

You can call this operation to modify the parameters of a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyDBClusterParameters.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster whose parameters are to be modified.|
|Parameters|String|Yes|The JSON strings of parameters and their values. All the parameter values are of the string type. For example, \{"auto\_increment":"1","character\_set\_client":"utf8"\}.

 |
|EffectiveTime|String|No|The time when the modified values of parameters take effect. Valid values: -   Auto: The system automatically determines how the modified values of parameters take effect. If all the modified values of parameters can take effect regardless of a cluster restart, they immediately take effect. If a cluster restart is required to make the modified values of some parameters take effect, all of them take effect after a cluster restart within the maintenance window.
-   Immediately: The modified values of parameters immediately take effect. If all the modified values of parameters can take effect regardless of a cluster restart, they immediately take effect. If a cluster restart is required to make the modified values of some parameters take effect, the cluster is immediately restarted to make all of them take effect.
-   MaintainTime: The modified values of parameters take effect within the maintenance window. No matter whether a cluster restart is required to make the modified values of parameters take effect, all of them take effect within the maintenance window.

 Default value: Auto.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_khc_1dz_xfb .section}

``` {#codeblock_xku_mik_t49}
https://polardb.aliyuncs.com/?Action=ModifyDBClusterParameters
&DBClusterId=pc-xxxxxxxxxx
&Parameters= {"auto_increment":"1","character_set_client":"utf8"}
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_dr4_vqw_xzu}
<ModifyDBClusterParametersResponse>  
    <RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</ModifyDBClusterParametersResponse>
```

JSON format

``` {#codeblock_ysl_7mn_adx}
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

