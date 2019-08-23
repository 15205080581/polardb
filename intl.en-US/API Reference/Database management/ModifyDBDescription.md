# ModifyDBDescription {#concept_h3q_rfd_ggb .concept}

You can call this operation to modify the description of a database for a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyDBDescription.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to which a database belongs.|
|DBName|String|Yes|The name of the database whose description is to be modified.|
|DBDescription|String|Yes|The description of the database.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ModifyDBDescription
&DBClusterId=pc-xxxxxxxxxxxxxxxxxxxx
&DBName=testDB
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<CheckDBNameResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</CheckDBNameResponse>
```

JSON format

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

