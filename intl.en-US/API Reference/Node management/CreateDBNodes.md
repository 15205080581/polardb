# CreateDBNodes {#reference_zpr_187230 .reference}

You can call this operation to add a node to a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to CreateDBNodes.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to be added a node to.|
|DBNode.N.ZoneId|String|No|The zone ID of the node to be added, which must be the same as that of existing nodes. N is an integer that starts from 1. The maximum value of N is equal to 16 minus the number of current nodes. You must specify either the DBNode.N.ZoneId or DBNode.N.TargetClass parameter. You can call the [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) operation to query available zones. **Note:** Currently, you add only a node at a time.

 |
|DBNode.N.TargetClass|String|No|The specifications of the node, which must be the same as those of existing nodes. N is an integer that starts from 1. The maximum value of N is equal to 16 minus the number of current nodes. You must specify either the DBNode.N.ZoneId or DBNode.N.TargetClass parameter. For more information about specifications, see [../../../../dita-oss-bucket/SP\_61/DNPOLA1875676/EN-US\_TP\_3012.md\#](../../../../intl.en-US/Pricing/Specifications and pricing.md#). **Note:** Currently, you add only a node at a time.

 |
|ClientToken|String|No|The client token that is used to ensure the idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The token is case-sensitive. It can contain only ASCII characters, and cannot exceed 64 characters in length.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|
|DBClusterId|String|The ID of the ApsaraDB for POLARDB cluster.|
|OrderId|String|The PO No. of the request.|

## Sample request {#section_khc_1dz_xfb .section}

``` {#codeblock_5pt_e5m_hgn}
https://polardb.aliyuncs.com/?Action=CreateDBNodes
&DBClusterId=pc-xxxxxxxxxx
&DBNode.N.TargetClass=polar.mysql.x2.medium
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_bbd_imn_w3e}
<CreateDBNodesResponse>  
    <OrderId>2035624xxxxxxxx</OrderId>
    <RequestId>C5BC3F8D-37C0-40EF-B5EF-457F983C612A</RequestId>
    <DBClusterId>pc-xxxxxxxxxxxxx</DBClusterId>
</CreateDBNodesResponse>
```

JSON format

``` {#codeblock_yfr_ysn_h5h}
{
    "OrderId": 2035624xxxxxxxx,
    "RequestId": "C5BC3F8D-37C0-40EF-B5EF-457F983C612A",
    "DBClusterId": "pc-xxxxxxxxxxxxx"
}
```

