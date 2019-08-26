# DescribeDBClusterAccessWhiteList {#reference_qhl_fn5_xfb .reference}

You can call this operation to query the IP address whitelist of a specified ApsaraDB for POLARDB cluster.

**Note:** Currently, POLARDB for PostgreSQL and POLARDB for Oracle do not support this operation.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeDBClusterAccessWhiteList.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to be queried.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|
|Items|List<DBClusterIPArray\>|The list of IP address whitelist groups of the cluster.|

## DBClusterIPArray {#section_ilc_b3s_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|DBClusterIPArrayAttribute|String|The attribute of the IP address whitelist group.|
|DBClusterIPArrayName|String|The name of the IP address whitelist group.|
|SecurityIps|String|The IP addresses in the IP address whitelist group. Each whitelist group can contain a maximum of 1,000 IP addresses. Multiple IP addresses are separated with a comma \(,\). The following two formats are supported: -   IP address: for example, 10.23.12.24.
-   Classless inter-domain routing \(CIDR\) block: for example, 10.23.12.24/24, where the suffix /24 indicates the number of bits for the prefix of the IP address. The suffix ranges from 1 to 32.

 |

## Sample request {#section_snj_c3s_xfb .section}

``` {#codeblock_862_e09_985}
https://polardb.aliyuncs.com/?Action=DescribeDBClusterAccessWhiteList
&DBClusterId=pc-xxxxxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_zib_gce_d9d}
<DescribeDBClusterAccessWhiteListResponse>  
    <Items>
        <DBClusterIPArray>
            <DBClusterIPArrayAttribute></DBClusterIPArrayAttribute>
            <DBClusterIPArrayName>default</DBClusterIPArrayName>
            <SecurityIPList>127.0.0.1</SecurityIPList>
        </DBClusterIPArray>
        <DBClusterIPArray>
            <DBClusterIPArrayAttribute>hidden</DBClusterIPArrayAttribute>
            <DBClusterIPArrayName>maxscale</DBClusterIPArrayName>
            <SecurityIPList>11.xx.xx.xx,11.xx.xx.xx</SecurityIPList>
        </DBClusterIPArray>
    </Items>
    <RequestId>8D0429EC-8E2C-4675-8102-28AC6FE92751</RequestId>
</DescribeDBClusterAccessWhiteListResponse>
```

JSON format

``` {#codeblock_s0i_tfs_lm6}
{
    "Items":{
        "DBClusterIPArray":[
            {
                "DBClusterIPArrayAttribute":"",
                "DBClusterIPArrayName":"default",
                "SecurityIPList":"127.0.0.1"
            },
            {
                "DBClusterIPArrayAttribute":"hidden",
                "DBClusterIPArrayName":"maxscale",
                "SecurityIPList":"11.xx.xx.xx,11.xx.xx.201"
            }
        ]
    },
    "RequestId":"8D0429EC-8E2C-4675-8102-28AC6FE92751"
}
```

