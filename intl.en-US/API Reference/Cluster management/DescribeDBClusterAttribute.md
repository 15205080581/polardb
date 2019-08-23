# DescribeDBClusterAttribute {#reference_p5z_535_xfb .reference}

You can call this operation to query the detailed information of a specified ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeDBClusterAttribute.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to be queried.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RegionId|String|The ID of the region.|
|DBClusterId|String|The ID of the ApsaraDB for POLARDB cluster.|
|DBClusterDescription|String|The description of the cluster.|
|PayType|String|The billing method of the cluster. Valid values: -   Postpaid: Pay-As-You-Go.
-   Prepaid: Subscription.

 |
|Engine|String|The engine of the cluster.|
|DBType|String|The type of the database.|
|DBVersion|String|The version of the database.|
|DBClusterStatus|String|The status of the cluster. For more information, see [Cluster states](intl.en-US/API Reference/Appendixes/Cluster states.md#).|
|LockMode|String|The lock mode of the cluster. Valid values: -   Unlock: The cluster is not locked.
-   ManualLock: The cluster is manually locked.
-   LockByExpiration: The cluster is automatically locked after it expires.

 |
|DBClusterNetworkType|String|The network type of the cluster.|
|VPCId|String|The VPC ID of the cluster.|
|VSwitchId|String|The VSwitch ID of the cluster.|
|StorageUsed|Long|The storage usage of the cluster, in bytes.|
|StorageMax|Long|The maximum storage capacity supported by the current specifications of the cluster, in bytes.|
|CreationTime|String|The time when the cluster was created. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format, for example, 2011-05-30T12:11:4Z.|
|ExpireTime|String|The time when the cluster expires. **Note:** Pay-As-You-Go clusters never expire.

 |
|MaintainTime|String|The maintenance window of the cluster. The time follows the HH:mmZ-HH:mmZ format.

 For example, the value 16:00Z-17:00Z indicates that the cluster can be maintained from 00:00 to 01:00 \(UTC+8\).

 |
|Expired|String|Whether the cluster has expired.|
|IsLatestVersion|Boolean|Whether the version of the cluster is the latest.|
|ZoneIds|String|The zone where data is distributed.|
|DBNodes|List<DBNode\>|The list of nodes in the cluster.|
|Tags|List<Tag\>|The list of tags.|

## DBNode {#section_lmx_xg5_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|DBNodeId|String|The ID of the node.|
|ZoneId|String|The zone ID of the node.|
|DBInstanceStatus|String|The status of the node.|
|CreationTime|String|The time when the node was created.|
|DBNodeClass|String|The specifications of the node.|
|DBNodeRole|String|The role of the node. Valid values: -   Writer
-   Reader

 |
|MaxIOPS|Integer|The maximum number of input/output operations per second \(IOPS\) supported by the node.|
|MaxConnections|Integer|The maximum number of concurrent connections supported by the node.|

## Tag {#section_yth_nv1_1hb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|Key|String|The key of the tag.|
|Value|String|The value of the tag.|

## Sample request {#section_snj_c3s_xfb .section}

``` {#codeblock_yqr_dbh_rkl}
https://polardb.aliyuncs.com/?Action=DescribeDBClusterAttribute
&DBClusterId=pc-xxxxxxxxxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_yed_qw5_24v}
<DescribeDBClusterAttributeResponse>  
    <DBVersion>5.6</DBVersion>
    <LockMode>Unlock</LockMode>
    <DBClusterDescription>test</DBClusterDescription>
    <DBClusterNetworkType>VPC</DBClusterNetworkType>
    <DBClusterId>pc-xxxxxxxxxxxxxx</DBClusterId>
    <VSwitchId>vsw-xxxxxxxxxxxxxx</VSwitchId>
    <Engine>POLARDB</Engine>
    <DBClusterStatus>Running</DBClusterStatus>
    <CreationTime>2019-04-26T06:01:28Z</CreationTime>
    <MaintainTime>18:00Z-19:00Z</MaintainTime>
    <VPCId>vpc-xxxxxxxxxxxxxx</VPCId>
    <ExpireTime></ExpireTime>
    <Expired>false</Expired>
    <RequestId>4E148395-950A-46F8-BFF8-274A64CD793B</RequestId>
    <RegionId>cn-qingdao</RegionId>
    <DBType>MySQL</DBType>
    <DBNodes>
        <CreationTime>2019-04-26T22:01:28Z</CreationTime>
        <MaxIOPS>8000</MaxIOPS>
        <DBNodeRole>Writer</DBNodeRole>
        <MaxConnections>1200</MaxConnections>
        <DBNodeClass>polar.mysql.x2.medium</DBNodeClass>
        <DBNodeStatus>Running</DBNodeStatus>
        <ZoneId>cn-qingdao-c</ZoneId>
        <DBNodeId>pi-xxxxxxxxxxxxxx</DBNodeId>
    </DBNodes>
    <DBNodes>
        <CreationTime>2019-04-26T22:01:28Z</CreationTime>
        <MaxIOPS>8000</MaxIOPS>
        <DBNodeRole>Reader</DBNodeRole>
        <MaxConnections>1200</MaxConnections>
        <DBNodeClass>polar.mysql.x2.medium</DBNodeClass>
        <DBNodeStatus>Running</DBNodeStatus>
        <ZoneId>cn-qingdao-c</ZoneId>
        <DBNodeId>pi-xxxxxxxxxxxxxx</DBNodeId>
    </DBNodes>
    <SQLSize>0</SQLSize>
    <PayType>Postpaid</PayType>
</DescribeDBClusterAttributeResponse>
```

JSON format

``` {#codeblock_9ic_8s3_a83}
{
    "DBVersion": "5.6",
    "LockMode": "Unlock",
    "DBClusterDescription": "test",
    "DBClusterNetworkType": "VPC",
    "DBClusterId": "pc-xxxxxxxxxxxxxx",
    "VSwitchId": "vsw-xxxxxxxxxxxxxx",
    "Engine": "POLARDB",
    "DBClusterStatus": "Running",
    "CreationTime": "2019-04-26T06:01:28Z",
    "MaintainTime": "18:00Z-19:00Z",
    "Tags": [],
    "VPCId": "vpc-xxxxxxxxxxxxxx",
    "ExpireTime": "",
    "Expired": false,
    "RequestId": "4E148395-950A-46F8-BFF8-274A64CD793B",
    "RegionId": "cn-qingdao",
    "DBType": "MySQL",
    "DBNodes": [
        {
            "CreationTime": "2019-04-26T22:01:28Z",
            "MaxIOPS": 8000,
            "DBNodeRole": "Writer",
            "MaxConnections": 1200,
            "DBNodeClass": "polar.mysql.x2.medium",
            "DBNodeStatus": "Running",
            "ZoneId": "cn-qingdao-c",
            "DBNodeId": "pi-xxxxxxxxxxxxxx"
        },
        {
            "CreationTime": "2019-04-26T22:01:28Z",
            "MaxIOPS": 8000,
            "DBNodeRole": "Reader",
            "MaxConnections": 1200,
            "DBNodeClass": "polar.mysql.x2.medium",
            "DBNodeStatus": "Running",
            "ZoneId": "cn-qingdao-c",
            "DBNodeId": "pi-xxxxxxxxxxxxxx"
        }
    ],
    "SQLSize": 0,
    "PayType": "Postpaid"
}
```

