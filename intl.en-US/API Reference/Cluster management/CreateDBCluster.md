# CreateDBCluster {#reference_nyk_pd5_xfb .reference}

You can call this operation to create an ApsaraDB for POLARDB cluster.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to CreateDBCluster.|
|RegionId|String|Yes|The ID of the region, which can be up to 50 characters in length. You can call the [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) operation to query available regions.|
|DBType|String|Yes|The type of the database. Valid values: -   MySQL
-   PostgreSQL
-   Oracle

 |
|DBVersion|String|Yes|The version of the database. Valid values: -   MySQL: 5.6 or 8.0
-   PostgreSQL: 11
-   Oracle: 11

 |
|DBNodeClass|String|Yes|The node specifications of the cluster. For more information, see [Specifications and pricing](../../../../intl.en-US/Pricing/Specifications and pricing.md#).|
|PayType|String|Yes|The billing method of the cluster. Valid values: -   Postpaid: pay-as-you-go
-   Prepaid: subscription

 |
|CreationOption|String|No|The method for creating an ApsaraDB for POLARDB cluster. Valid values: -   Normal: creates an ApsaraDB for POLARDB cluster.
-   CloneFromPolarDB: clones data from an existing ApsaraDB for POLARDB cluster to a new ApsaraDB for POLARDB cluster.
-   CloneFromRDS: clones data from an existing ApsaraDB for RDS instance to a new ApsaraDB for POLARDB cluster.
-   MigrationFromRDS: migrates data from an existing ApsaraDB for RDS instance to a new ApsaraDB for POLARDB cluster. The created ApsaraDB for POLARDB cluster is in read-only mode and has binary logs enabled by default.

 Default value: Normal.

 **Note:** This parameter takes effect only when the **DBType** parameter is set to **MySQL** and the **DBVersion** parameter is set to **5.6**.

 |
|SourceResourceId|String|No|The ID of the source RDS instance or source POLARDB cluster. **Note:** 

-   This parameter takes effect only when the **DBType** parameter is set to **MySQL** and the **DBVersion** parameter is set to **5.6**.
-   This parameter is required if the **CreationOption** parameter is not set to **Normal**.

 |
|CloneDataPoint|String|No|The time point of data to be cloned. Valid values: -   LATEST: clones data of the latest time point.
-   <BackupID\>: clones historical backup data. Specify the ID of the specific backup set.
-   <Timestamp\>: clones data of a historical time point. Specify the specific time in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

 Default value: LATEST.

 **Note:** 

-   This parameter takes effect only when the **DBType** parameter is set to **MySQL**, the **DBVersion** parameter is set to **5.6**, and the **CreationOption** parameter is set to **CloneFromRDS** or **CloneFromPolarDB**.
-   If the **CreationOption** parameter is set to **CloneFromRDS**, the value of this parameter must be **LATEST**.

 |
|ZoneId|String|No|The zone ID of the cluster. You can call the [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) operation to query available zones.|
|ClusterNetworkType|String|No|The network type of the cluster. Currently, only VPC is supported. Default value: VPC.|
|VPCId|String|No|The ID of the VPC to connect to.|
|VSwitchId|String|No|The ID of the VSwitch to connect to.|
|DBClusterDescription|String|No|The description of the cluster. The description must comply with the following rules: -   It must start with a Chinese character or an English letter.
-   It can contain Chinese and English characters, digits, underscores \(\_\), and hyphens \(-\).
-   It cannot start with http:// or https://.
-   It must be 2 to 256 characters in length.

 |
|AutoRenew|String|No|Specifies whether to enable auto renewal. Valid values: -   true: enables auto renewal.
-   false: disables auto renewal.

 Default value: false.

 **Note:** This parameter takes effect only when the PayType parameter is set to Prepaid.

 |
|Period|String|No|The unit of the subscription period. This parameter is required if the PayType parameter is set to Prepaid. Valid values: -   Year: subscription on a yearly basis
-   Month: subscription on a monthly basis

 |
|UsedTime|String|No| -   The subscription period of the cluster. The valid values depend on the value specified in the Period parameter. Valid values:
-   Month: \[1, 9\]
-   Year: \[1, 3\]

 |
|ClientToken|String|No|The client token that is used to ensure the idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The token is case-sensitive. It can contain only ASCII characters, and cannot exceed 64 characters in length.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|RequestId|String|The ID of the request.|
|DBClusterId|String|The ID of the ApsaraDB for POLARDB cluster.|
|OrderId|String|The PO No. of the request.|

## Sample request {#section_lx1_c25_xfb .section}

``` {#codeblock_8o4_gey_4x0}
https://polardb.aliyuncs.com/?Action=CreateDBCluster
&RegionId=cn-hangzhou
&DBType=MySQL
&DBVersion=5.6
&DBNodeClass=polar.mysql.x2.medium
&PayType=Postpaid
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

``` {#codeblock_l1z_fic_ulu}
<CreateDBClusterResponse>  
    <RequestId>E056BF3D-1E4F-4E39-B729-8491A74B301B</RequestId>
    <OrderId>20235327xxxxx</OrderId>
    <DBClusterId>pc-xxxxxxxxxxxxx</DBClusterId>
</CreateDBClusterResponse>
```

JSON format

``` {#codeblock_jq4_n7c_78t}
{
  "RequestId": "E056BF3D-1E4F-4E39-B729-8491A74B301B",
  "OrderId": "20235327xxxxx",
  "DBClusterId": "pc-xxxxxxxxxxxxxxx"
}
```

