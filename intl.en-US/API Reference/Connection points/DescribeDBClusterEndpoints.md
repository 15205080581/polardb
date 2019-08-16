# DescribeDBClusterEndpoints {#reference_gkh_gbz_xfb .reference}

You can call this operation to query the connection point information of a specified ApsaraDB for POLARDB cluster.

**Note:** Currently, POLARDB for PostgreSQL and POLARDB for Oracle do not support this operation.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeDBClusterEndpoints.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to be queried.|
|DBEndpointId|String|No|The ID of the cluster connection point to be queried. For example, pe-xxxxxxxx.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|
|Items|List<DBEndpoint\>|The list of cluster connection points.|

## DBEndpoint {#section_ejf_mbz_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|DBEndpointId|String|The ID of the cluster connection point.|
|EndpointType|String|The type of the cluster connection point. Valid values: -   Cluster: the default connection point of the cluster.
-   Primary: the primary endpoint of the cluster.
-   Custom: the custom connection point of the cluster.

 |
|AutoAddNewNodes|String|Indicates whether a newly added node is automatically added to this connection point. Valid values: -   Enable
-   Disable

 |
|ReadWriteMode|String|The read/write mode of the cluster connection point. Valid values: -   ReadWrite: receives and forwards read and write requests \(automatic read-write splitting\).
-   ReadOnly: receives and forwards only read requests.

 |
|Nodes|String| -   The nodes that were added to this connection point. Valid values: Auto, which indicates that nodes were automatically selected based on the cluster connection point type.
-   A custom list of node IDs that are separated with a comma \(,\).

 |
|EndpointConfig|String|The consistency level of the cluster connection point. Valid values: -   0: eventual consistency
-   1: session consistency

 |
|AddressItems|List<Address\>|The information about the cluster connection point.|

## Address {#section_sdq_qbz_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|ConnectionString|String|The connection string of the cluster connection point.|
|IPAddress|String|The IP address of the cluster connection point.|
|Port|String|The port number of the cluster connection point.|
|NetType|String|The network type of the cluster connection point. Valid values: -   Public: public network
-   Private: private network

 |
|VPCId|String|The VPC ID of the cluster connection point.|
|VSwitchId|String|The VSwitch ID of the cluster connection point.|

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeDBClusterEndpoints
&DBClusterId=pc-xxxxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<DescribeDBClusterEndpointsResponse>  
    <Items>
        <EndpointType>Primary</EndpointType>
        <AddressItems>
            <Port>3306</Port>
            <ConnectionString>pc-xxxxxxxxxx.w.polardb.cn-qd-pldb1.rds.aliyuncs.com</ConnectionString>
            <VPCId>vpc-xxxxxxxxxx</VPCId>
            <IPAddress>172.xx.xx.xx</IPAddress>
            <NetType>Private</NetType>
            <VSwitchId>vsw-xxxxxxxxxx</VSwitchId>
        </AddressItems>
        <Nodes>pi-xxxxxxxxxx</Nodes>
        <DBEndpointId>pe-xxxxxxxxxx</DBEndpointId>
        <EndpointConfig>{}</EndpointConfig>
    </Items>
    <Items>
        <EndpointType>Cluster</EndpointType>
        <AutoAddNewNodes>Enable</AutoAddNewNodes>
        <ReadWriteMode>ReadWrite</ReadWriteMode>
        <AddressItems>
            <Port>3306</Port>
            <ConnectionString>pc-xxxxxxxxxx.polardb.cn-qd-pldb1.rds.aliyuncs.com</ConnectionString>
            <VPCId>vpc-xxxxxxxxxx</VPCId>
            <IPAddress>172.xx.xx.xx</IPAddress>
            <NetType>Private</NetType>
            <VSwitchId>vsw-xxxxxxxxxx</VSwitchId>
        </AddressItems>
        <Nodes>pi-xxxxxxxxxx,pi-xxxxxxxxxx</Nodes>
        <DBEndpointId>pe-xxxxxxxxxx</DBEndpointId>
        <EndpointConfig>{&quot;ConsistLevel&quot;:&quot;1&quot;,&quot;CausalConsistRead&quot;:&quot;1&quot;,&quot;LoadBalanceStrategy&quot;:&quot;load&quot;}</EndpointConfig>
    </Items>
    <Items>
        <EndpointType>Custom</EndpointType>
        <AutoAddNewNodes>Disable</AutoAddNewNodes>
        <ReadWriteMode>ReadOnly</ReadWriteMode>
        <AddressItems>
            <Port>3306</Port>
            <ConnectionString>pe-xxxxxxxxxx.polardb.cn-qd-pldb1.rds.aliyuncs.com</ConnectionString>
            <VPCId>vpc-xxxxxxxxxx</VPCId>
            <IPAddress>172.xx.xx.xx</IPAddress>
            <NetType>Private</NetType>
            <VSwitchId>vsw-xxxxxxxxxx</VSwitchId>
        </AddressItems>
        <Nodes>pi-xxxxxxxxxx,pi-xxxxxxxxxx</Nodes>
        <DBEndpointId>pe-xxxxxxxxxx</DBEndpointId>
        <EndpointConfig>{&quot;ConsistLevel&quot;:&quot;0&quot;,&quot;CausalConsistRead&quot;:&quot;0&quot;,&quot;LoadBalanceStrategy&quot;:&quot;load&quot;}</EndpointConfig>
    </Items>
    <RequestId>ABA96273-606B-4616-9394-336A06312713</RequestId>
</DescribeDBClusterEndpointsResponse>
```

JSON format

```
{
    "Items": [
        {
            "EndpointType": "Primary",
            "AddressItems": [
                {
                    "Port": "3306",
                    "ConnectionString": "pc-xxxxxxxxxx.w.polardb.cn-qd-pldb1.rds.aliyuncs.com",
                    "VPCId": "vpc-xxxxxxxxxx",
                    "IPAddress": "172.xx.xx.xx",
                    "NetType": "Private",
                    "VSwitchId": "vsw-xxxxxxxxxx"
                }
            ],
            "Nodes": "pi-xxxxxxxxxx",
            "DBEndpointId": "pe-xxxxxxxxxx",
            "EndpointConfig": "{}"
        },
        {
            "EndpointType": "Cluster",
            "AutoAddNewNodes": "Enable",
            "ReadWriteMode": "ReadWrite",
            "AddressItems": [
                {
                    "Port": "3306",
                    "ConnectionString": "pc-xxxxxxxxxx.polardb.cn-qd-pldb1.rds.aliyuncs.com",
                    "VPCId": "vpc-xxxxxxxxxx",
                    "IPAddress": "172.xx.xx.xx",
                    "NetType": "Private",
                    "VSwitchId": "vsw-xxxxxxxxxx"
                }
            ],
            "Nodes": "pi-xxxxxxxxxx,pi-xxxxxxxxxx",
            "DBEndpointId": "pe-xxxxxxxxxx",
            "EndpointConfig": "{\"ConsistLevel\":\"1\",\"CausalConsistRead\":\"1\",\"LoadBalanceStrategy\":\"load\"}"
        },
        {
            "EndpointType": "Custom",
            "AutoAddNewNodes": "Disable",
            "ReadWriteMode": "ReadOnly",
            "AddressItems": [
                {
                    "Port": "3306",
                    "ConnectionString": "pe-xxxxxxxxxx.polardb.cn-qd-pldb1.rds.aliyuncs.com",
                    "VPCId": "vpc-xxxxxxxxxx",
                    "IPAddress": "172.xx.xx.xx",
                    "NetType": "Private",
                    "VSwitchId": "vsw-xxxxxxxxxx"
                }
            ],
            "Nodes": "pi-xxxxxxxxxx,pi-xxxxxxxxxx",
            "DBEndpointId": "pe-xxxxxxxxxx",
            "EndpointConfig": "{\"ConsistLevel\":\"0\",\"CausalConsistRead\":\"0\",\"LoadBalanceStrategy\":\"load\"}"
        }
    ],
    "RequestId": "ABA96273-606B-4616-9394-336A06312713"
}
```

