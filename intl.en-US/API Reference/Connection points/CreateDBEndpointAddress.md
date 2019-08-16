# CreateDBEndpointAddress {#reference_rpf_ndz_xfb .reference}

You can call this operation to create a public connection point for a specified ApsaraDB for POLARDB cluster.

**Note:** Currently, POLARDB for PostgreSQL and POLARDB for Oracle do not support public connection points.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to CreateDBEndpointAddress.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster for which a public connection point is to be created.|
|DBEndpointId|String|Yes|The ID of the cluster connection point. **Note:** You can call the [DescribeDBClusterEndpoints](intl.en-US/API Reference/Connection points/DescribeDBClusterEndpoints.md#) to query available cluster connection points.

 |
|ConnectionStringPrefix|String|Yes|The prefix of the connection string. The prefix must comply with the following rules: -   It must start with a letter and consist of lowercase letters, digits, and hyphens \(-\).
-   It can be up to 30 characters in length.

 |
|NetType|String|Yes|The network type of the connection string. Currently, only the public network is supported. Set this parameter to Public.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_khc_1dz_xfb .section}

``` {#codeblock_d4t_96h_duh}
https://polardb.aliyuncs.com/?Action=CreateDBEndpointAddress
&DBClusterId=pc-xxxxxxxxxxxxxx
&DBEndpointId=pe-xxxxxxxxxxxxx
&ConnectionStringPrefix=pc-xxxxxxxxxxxx-pub
&NetType=Public
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_t0b_k5q_73i}
<CreateDBEndpointAddressResponse>  
    <RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</CreateDBEndpointAddressResponse>
```

JSON format

``` {#codeblock_3qe_kdp_o0v}
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

