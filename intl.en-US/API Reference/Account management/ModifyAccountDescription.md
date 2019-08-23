# ModifyAccountDescription {#reference_yqb_s1t_xfb .reference}

You can call this operation to modify the description of a database account for a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyAccountDescription.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to which a database account belongs.|
|AccountName|String|Yes|The name of the database account whose description is to be modified.|
|AccountDescription|String|Yes|The description of the database account. The description must comply with the following rules: -   It must start with a Chinese character or an English letter.
-   It can contain Chinese and English characters, digits, underscores \(\_\), and hyphens \(-\).
-   It cannot start with http:// or https://.
-   It must be 2 to 256 characters in length.

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=ModifyAccountDescription
&DBClusterId=pc-xxxxxxxxxxxxxxxx
&AccountName=testacc
&AccountDescription=AccDesc
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<ModifyAccountDescriptionResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</ModifyAccountDescriptionResponse>
```

JSON format

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

