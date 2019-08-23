# ModifyDBClusterAccessWhiteList {#reference_vrz_3m5_xfb .reference}

You can call this operation to modify the IP address whitelist of a specified ApsaraDB for POLARDB cluster.

**Note:** Currently, POLARDB for PostgreSQL and POLARDB for Oracle do not support this operation.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to ModifyDBClusterAccessWhiteList.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster whose IP address whitelist is to be modified.|
|SecurityIps|String|Yes|The IP addresses to be added to the IP address whitelist group to be modified. Each whitelist group can contain a maximum of 1,000 IP addresses. Separate multiple IP addresses with a comma \(,\). The following two formats are supported: -   IP address: for example, 10.23.12.24.
-   Classless inter-domain routing \(CIDR\) block: for example, 10.23.12.24/24, where the suffix /24 indicates the number of bits for the prefix of the IP address. The suffix ranges from 1 to 32.

 |
|DBClusterIPArrayName|String|No|The name of the IP address whitelist group. If you do not specify this parameter, the **Default** whitelist group is modified by default. **Note:** You can create up to 50 whitelist groups for an ApsaraDB for POLARDB cluster.

 |

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|

## Sample request {#section_snj_c3s_xfb .section}

``` {#codeblock_8pq_zgk_dbd}
https://polardb.aliyuncs.com/?Action=ModifyDBClusterAccessWhiteList
&DBClusterId=pc-xxxxxxxxx
&SecurityIps=127.0.0.1
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_j2q_tnz_15v}
<ModifyDBClusterAccessWhiteListResponse>  
    <RequestId>D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC</RequestId>
</ModifyDBClusterAccessWhiteListResponse>
```

JSON format

``` {#codeblock_vib_jay_149}
{
  "RequestId": "D0CEC6AC-7760-409A-A0D5-E6CD8660E9CC"
}
```

