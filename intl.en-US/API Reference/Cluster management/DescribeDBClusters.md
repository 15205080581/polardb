# DescribeDBClusters {#reference_edc_zls_xfb .reference}

You can call this operation to query ApsaraDB for POLARDB clusters or ApsaraDB for POLARDB clusters whose permissions are granted to a RAM user.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeDBClusters.|
|RegionId|String|Yes|The ID of the region.|
|DBClusterIds|String|No|The ID of the ApsaraDB for POLARDB cluster. Separate multiple cluster IDs with a comma \(,\).|
|DBClusterDescription|String|No|The description of the cluster, which supports fuzzy query.|
|DBClusterStatus|String|No|The status of the cluster. For more information, see [Cluster states](intl.en-US/API Reference/Appendixes/Cluster states.md#).|
|DBType|String|No|The type of the database. Valid values: -   MySQL
-   PostgreSQL
-   Oracle

 |
|Tag.n.Key|String|No|The key of the tag that you can use to filter clusters by tag. You can specify up to 20 key-value pairs of tags at a time. The number n in each key-value pair must be different and must be consecutive integers that start from 1. Each value of the Tag.n.Key parameter is paired with a value of the Tag.n.Value parameter. **Note:** Each value of this parameter can be up to 64 characters in length. It cannot start with **aliyun**, **acs:**, **http://**, or **https://**.

 |
|Tag.n.Value|String|No|The value of the tag that you can use to filter clusters by tag. You can specify up to 20 key-value pairs of tags at a time. The number n in each key-value pair must be different and must be consecutive integers that start from 1. Each value of the Tag.n.Value parameter is paired with a value of the Tag.n.Key parameter. **Note:** 

-   If you specify the **Tag.n.Key** parameter, you must also specify the **Tag.n.Value** parameter.
-   Each value of this parameter can be up to 64 characters in length. It cannot start with **aliyun**, **acs:**, **http://**, or **https://**.

 |
|PageSize|Integer|No|The number of entries to return on each page. Valid values: -   30
-   50
-   100

 Default value: 30.

 |
|PageNumber|Integer|No|The number of the page to return. Valid values: any non-zero positive integer. Default value: 1.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|
|PageNumber|Integer|The number of the page returned.|
|TotalRecordCount|Integer|The total number of entries returned.|
|PageRecordCount|Integer|The total number of pages returned.|
|Items|List<DBCluster\>|The list of clusters.|

## DBCluster {#section_ilc_b3s_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|DBClusterId|String|The ID of the ApsaraDB for POLARDB cluster.|
|DBClusterDescription|String|The description of the cluster.|
|PayType|String|The billing method of the cluster. Valid values: -   Postpaid: Pay-As-You-Go.
-   Prepaid: Subscription.

 |
|RegionId|String|The ID of the region.|
|CreateTime|String|The time when the cluster was created.|
|ExpireTime|String|The time when the cluster expires.|
|DBClusterStatus|String|The status of the cluster.|
|Engine|String|The engine of the cluster.|
|DBType|String|The type of the database.|
|DBVersion|String|The version of the database.|
|LockMode|String|The lock mode of the cluster. Valid values: -   Unlock: The cluster is not locked.
-   ManualLock: The cluster is manually locked.
-   LockByExpiration: The cluster is automatically locked after it expires.

 |
|DBClusterNetworkType|String|The network type of the cluster.|
|VPCId|String|The VPC ID of the cluster.|
|DBNodeNumber|Integer|The number of nodes.|
|DBNodeClass|String|The specifications of the primary node.|
|StorageUsed|Long|The storage usage of the cluster.|
|Tags|List<Tag\>|The list of tags.|
|DBNodes|List<DBNode\>|The list of nodes in the cluster.|
|DeletionLock|Integer|Whether to lock the deletion operation. -   0: not locked.
-   1: locked.

 |
|Expired|String|Whether the cluster has expired.|

## DBNode {#section_crc_fns_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|DBNodeId|String|The ID of the node.|
|DBNodeClass|String|The specifications of the node.|
|DBNodeRole|String|The role of the node. Valid values: -   Writer
-   Reader

 |
|ZoneId|String|The ID of the zone where the node is located.|

## Tag {#section_2sf_yb0_gty .section}

|Parameter|Type|Description|
|---------|----|-----------|
|Key|String|The key of the tag.|
|Value|String|The value of the tag.|

## Sample request {#section_snj_c3s_xfb .section}

``` {#codeblock_912_4mk_9eq}
https://polardb.aliyuncs.com/?Action=DescribeDBClusters
&RegionId=cn-hangzhou
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_a7c_vcc_chi}
<DescribeDBClustersResponse>  
    <Items>
        <DBCluster>
            <DBVersion>5.6</DBVersion>
            <LockMode>Unlock</LockMode>
            <DBClusterDescription>pc-xxxxxxxxxxxxxxxxx</DBClusterDescription>
            <DBClusterNetworkType>VPC</DBClusterNetworkType>
            <StorageUsed>3150970880</StorageUsed>
            <DBClusterId>pc-xxxxxxxxxxxxxxxxx</DBClusterId>
            <VpcId>vpc-xxxxxxxxxxxxxxxxx</VpcId>
            <Engine>POLARDB</Engine>
            <DBClusterStatus>Running</DBClusterStatus>
            <Tags>
                <Tag>
                    <Value>1111</Value>
                    <Key>test1</Key>
                </Tag>
                <Tag>
                    <Value>2222</Value>
                    <Key>test2</Key>
                </Tag>
            </Tags>
            <ExpireTime></ExpireTime>
            <DBNodeClass>polar.mysql.x4.large</DBNodeClass>
            <RegionId>cn-hangzhou</RegionId>
            <Expired>false</Expired>
            <CreateTime>2019-01-10T09:33:58Z</CreateTime>
            <DBType>MySQL</DBType>
            <DBNodes>
                <DBNode>
                    <DBNodeRole>Writer</DBNodeRole>
                    <DBNodeClass>polar.mysql.x4.large</DBNodeClass>
                    <DBNodeId>pi-xxxxxxxxxxxxxxxxx</DBNodeId>
                </DBNode>
                <DBNode>
                    <DBNodeRole>Reader</DBNodeRole>
                    <DBNodeClass>polar.mysql.x4.large</DBNodeClass>
                    <DBNodeId>pi-xxxxxxxxxxxxxxxxx</DBNodeId>
                </DBNode>
            </DBNodes>
            <DBNodeNumber>2</DBNodeNumber>
            <PayType>Postpaid</PayType>
        </DBCluster>
    </Items>
    <TotalRecordCount>1</TotalRecordCount>
    <PageNumber>1</PageNumber>
    <RequestId>F7036AE7-20B7-43F8-9E58-558CCDED8CCB</RequestId>
    <PageRecordCount>1</PageRecordCount>
  </DescribeDBClustersResponse>
```

JSON format

``` {#codeblock_brm_120_jbr}
{
    "Items": {
        "DBCluster": [
            {
                "DBVersion": "5.6",
                "LockMode": "Unlock",
                "DBClusterDescription": "pc-xxxxxxxxxxxxxxxxx",
                "DBClusterNetworkType": "VPC",
                "StorageUsed": 3150970880,
                "DBClusterId": "pc-xxxxxxxxxxxxxxxxx",
                "VpcId": "vpc-xxxxxxxxxxxxxxxxx",
                "Engine": "POLARDB",
                "DBClusterStatus": "Running",
                "Tags": {
                    "Tag": [
                        {
                            "Value": "1111",
                            "Key": "test1"
                        },
                        {
                            "Value": "2222",
                            "Key": "test2"
                        }
                    ]
                },
                "ExpireTime": "",
                "DBNodeClass": "polar.mysql.x4.large",
                "RegionId": "cn-hangzhou",
                "Expired": false,
                "CreateTime": "2019-01-10T09:33:58Z",
                "DBType": "MySQL",
                "DBNodes": {
                    "DBNode": [
                        {
                            "DBNodeRole": "Writer",
                            "DBNodeClass": "polar.mysql.x4.large",
                            "DBNodeId": "pi-xxxxxxxxxxxxxxxxx"
                        },
                        {
                            "DBNodeRole": "Reader",
                            "DBNodeClass": "polar.mysql.x4.large",
                            "DBNodeId": "pi-xxxxxxxxxxxxxxxxx"
                        }
                    ]
                },
                "DBNodeNumber": "2",
                "PayType": "Postpaid"
            }
        ]
    },
    "TotalRecordCount": 1,
    "PageNumber": 1,
    "RequestId": "F7036AE7-20B7-43F8-9E58-558CCDED8CCB",
    "PageRecordCount": 1
}
```

