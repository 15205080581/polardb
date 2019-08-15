# DescribeDBClusters {#reference_edc_zls_xfb .reference}

该接口用于查询POLARDB集群列表或被RAM授权的集群列表。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeDBClusters。|
|RegionId|String|是|地域ID。|
|DBClusterIds|String|否|如果有多个集群ID，以","分隔。|
|DBClusterDescription|String|否|集群描述，可模糊查询。|
|DBClusterStatus|String|否|集群状态，详见[集群状态表](cn.zh-CN/API参考/附表/集群状态表.md#)。|
|DBType|String|否|数据库类型，取值： -   MySQL；
-   PostgreSQL；
-   Oracle。

 |
|Tag.n.Key|String|否|标签键，可以根据标签过滤集群列表。最多20对标签，各个标签对的数字n必须不同，且必须是从1开始的连续整数。Tag.n.Key对应的值为Tag.n.Value。 **说明：** 最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。

 |
|Tag.n.Value|String|否|标签值，可以根据标签过滤集群列表。最多20对标签，各个标签对的数字n必须不同，且必须是从1开始的连续整数。Tag.n.Value是Tag.n.Key的值。 **说明：** 

-   若传入**Tag.n.Key**，则**Tag.n.Value**不能为空。
-   最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。

 |
|PageSize|Integer|否|每页记录数，取值： -   30；
-   50；
-   100。

 默认值：30。

 |
|PageNumber|Integer|否|页码，取值为：大于0且不超过Integer数据类型的最大值，默认值为1。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)。|
|RequestId|String|RequestId。|
|PageNumber|Integer|页数。|
|TotalRecordCount|Integer|总记录数。|
|PageRecordCount|Integer|总页数。|
|Items|List<DBCluster\>|集群列表。|

## DBCluster参数 {#section_ilc_b3s_xfb .section}

|参数|类型|描述|
|:-|:-|:-|
|DBClusterId|String|数据库集群ID。|
|DBClusterDescription|String|集群描述。|
|PayType|String|付费类型： -   Postpaid：按量付费；
-   Prepaid：预付费（包年包月）。

 |
|RegionId|String|地域ID。|
|CreateTime|String|创建时间。|
|ExpireTime|String|到期时间。|
|DBClusterStatus|String|集群状态。|
|Engine|String|集群引擎。|
|DBType|String|数据库类型。|
|DBVersion|String|数据库版本。|
|LockMode|String|集群的锁定状态： -   Unlock：正常；
-   ManualLock：手动触发锁定；
-   LockByExpiration：集群过期自动锁定。

 |
|DBClusterNetworkType|String|集群的网络类型。|
|VPCId|String|专有网络ID。|
|DBNodeNumber|Integer|节点数量。|
|DBNodeClass|String|主节点规格。|
|StorageUsed|Long|存储用量。|
|Tags|List<Tag\>|标签列表。|
|DBNodes|List<DBNode\>|节点列表。|

## DBNode参数 {#section_crc_fns_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|DBNodeId|String|节点ID。|
|DBNodeClass|String|节点规格。|
|DBNodeRole|String|节点角色： -   Writer；
-   Reader。

 |

## Tag参数 {#section_2sf_yb0_gty .section}

|名称|类型|描述|
|--|--|--|
|Key|String|标签键。|
|Value|String|标签值。|

## 请求示例 {#section_snj_c3s_xfb .section}

``` {#codeblock_0bn_sal_ag9}
https://polardb.aliyuncs.com/?Action=DescribeDBClusters
&RegionId=cn-hangzhou
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_sgq_g2p_807}
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

JSON格式

``` {#codeblock_dcj_zjd_lkj}
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

