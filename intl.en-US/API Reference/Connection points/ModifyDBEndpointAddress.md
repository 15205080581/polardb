# ModifyDBEndpointAddress {#reference_rwk_tdz_xfb .reference}

You can call this operation to modify the prefix of the default connection point for a specified ApsaraDB for POLARDB cluster.

**Note:** Currently, POLARDB for PostgreSQL and POLARDB for Oracle do not support this operation.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyDBEndpointAddress.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to which a default connection point belongs.|
|EndpointId|String|Yes|The ID of the default connection point whose prefix is to be modified. For example, pe-xxxxxxxx.|
|NetType|String|Yes|The network type of the cluster connection point. Valid values: -   Public: public network
-   Private: private network

 |
|ConnectionStringPrefix|String|No|The prefix of the connection string. The prefix must comply with the following rules: -   It cannot end with a hyphen \(-\).
-   It must start with a letter and consist of lowercase letters, digits, and hyphens \(-\).
-   It must be more than six characters in length.

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_khc_1dz_xfb .section}

``` {#codeblock_h4m_o5g_h9w}
https://polardb.aliyuncs.com/?Action=ModifyDBEndpointAddress
&DBClusterId=pc-xxxxxxxxxx
&DBEndpointId=pe-xxxxxxxxxx
&ConnectionStringPrefix=pc-xxxxxxxxxx-pub2
&NetType=Public
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_mv7_to0_28x}
<CreateDBEndpointAddressResponse>  
    <RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</CreateDBEndpointAddressResponse>
```

JSON format

``` {#codeblock_kax_luv_jcv}
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

