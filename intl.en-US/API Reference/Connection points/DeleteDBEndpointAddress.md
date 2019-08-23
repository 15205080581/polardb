# DeleteDBEndpointAddress {#reference_wzw_12z_xfb .reference}

You can call this operation to release a public connection point for a specified ApsaraDB for POLARDB cluster.

**Note:** For more information about how to release a custom connection point for a specified ApsaraDB for POLARDB cluster, see [DeleteDBClusterEndpoint](intl.en-US/API Reference/Connection points/DeleteDBClusterEndpoint.md#).

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DeleteDBEndpointAddress.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to which a public connection point belongs.|
|EndpointId|String|Yes|The ID of the public connection point to be released. For example, pe-xxxxxxxx.|
|NetType|String|Yes|The network type of the cluster connection point. Valid values: -   Public: public network
-   Private: private network

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_khc_1dz_xfb .section}

``` {#codeblock_j28_loq_21j}
https://polardb.aliyuncs.com/?Action=DeleteDBEndpointAddress
&DBClusterId=pc-xxxxxxxxxx
&DBEndpointId=pe-xxxxxxxxxx
&NetType=Public
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_jiq_fcc_3jr}
<DeleteDBEndpointAddressResponse>  
    <RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</DeleteDBEndpointAddressResponse>
```

JSON format

``` {#codeblock_9bj_7n2_5lf}
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

