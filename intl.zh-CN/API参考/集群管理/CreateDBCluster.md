# CreateDBCluster {#reference_nyk_pd5_xfb .reference}

该接口用于创建POLARDB集群。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：CreateDBCluster。|
|RegionId|String|是|地域ID，长度不超过50个字符，通过接口[DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#)查看可用的地域。|
|DBType|String|是|数据库类型，取值： -   MySQL；
-   PostgreSQL；
-   Oracle。

 |
|DBVersion|String|是|数据库版本号，取值： -   MySQL：5.6/8.0；
-   PostgreSQL：11；
-   Oracle：11。

 |
|DBNodeClass|String|是|节点规格，参见[规格与定价](../../../../intl.zh-CN/产品定价/规格与定价.md#)。|
|PayType|String|是|付费类型： -   Postpaid：按量付费；
-   Prepaid：预付费（包年包月）。

 |
|CreationOption|String|否|创建方式，取值： -   Normal：创建一个全新的POLARDB集群，控制台操作请参见如下文档：
    -   [创建POLARDB for MySQL数据库集群](../../../../intl.zh-CN/POLARDB for MySQL快速入门/创建POLARDB for MySQL数据库集群.md#)
-   CloneFromPolarDB：从现有POLARDB集群克隆数据到新的POLARDB集群，控制台操作请参见如下文档：
    -   [恢复POLARDB for MySQL数据](../../../../intl.zh-CN/POLARDB for MySQL用户指南/备份与恢复/恢复数据.md#)
-   CloneFromRDS：从现有RDS实例克隆数据到新的POLARDB集群，控制台操作请参见[一键克隆RDS for MySQL到POLARDB for MySQL](../../../../intl.zh-CN/数据迁移__同步/POLARDB for MySQL/数据迁移/一键克隆RDS for MySQL到POLARDB for MySQL.md#)；
-   MigrationFromRDS：从现有RDS实例迁移数据到新的POLARDB集群。创建的POLARDB集群是只读模式，且默认开启Binlog。控制台操作请参见[一键升级RDS for MySQL到POLARDB for MySQL](../../../../intl.zh-CN/数据迁移__同步/POLARDB for MySQL/数据迁移/一键升级RDS for MySQL到POLARDB for MySQL.md#)。

 默认为Normal。

 **说明：** **DBType**=**MySQL**且**DBVersion****=5.6**时，本参数取值可以为**CloneFromRDS**或**MigrationFromRDS**。

 |
|SourceResourceId|String|否|源RDS实例ID或源POLARDB集群ID。 **说明：** 

-   **DBType**=**MySQL**且**DBVersion****=5.6**时，本参数有意义。
-   如果**CreationOption**≠**Normal**，本参数必填。

 |
|CloneDataPoint|String|否|克隆数据的时间节点，取值： -   LATEST：最新时间点的数据；
-   <BackupID\>：历史备份集ID，请传入具体的备份集ID；
-   <Timestamp\>：历史时间点，请传入具体的时间，格式：yyyy-MM-ddTHH:mm:ssZ（UTC时间）。

 默认为LATEST。

 **说明：** 

-   **DBType**=**MySQL**且**DBVersion****=5.6**，并且**CreationOption**=**CloneFromRDS**或**CloneFromPolarDB**本参数有意义。
-   如果**CreationOption**=**CloneFromRDS**，本参数取值只能为**LATEST**。

 |
|ZoneId|String|否|可用区ID，通过函数[DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#)查看可用的可用区。|
|ClusterNetworkType|String|否|当前仅支持VPC，默认VPC。|
|VPCId|String|否|专有网络ID。|
|VSwitchId|String|否|虚拟交换机ID。|
|DBClusterDescription|String|否|集群描述： -   以中文、英文字母开头；
-   可以包含中文、英文字符、数字、”，”、” -”；
-   不能以http://，https开头；
-   长度为2-256个字符。

 |
|AutoRenew|String|否|是否自动续费： -   true：自动续费；
-   false：不自动续费。

 默认为false。

 **说明：** 当参数PayType取值为PrePaid时才生效。

 |
|Period|String|否|若付费类型为Prepaid时，该参数为必传参数。指定预付费集群为包年或包月类型。 -   Year：包年；
-   Month：包月。

 |
|UsedTime|String|否| -   当Period为Month时，UsedTime取值为\[1-9\]。
-   当Period为Year时，UsedTime取值为\[1-3\]。

 |
|ClientToken|String|否|用于保证请求的幂等性。由客户端生成该参数值，保证在不同请求间唯一，大小写敏感、不超过64个 ASCII 字符。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)|
|RequestId|String|RequestId。|
|DBClusterId|String|数据库集群ID。|
|OrderId|String|订单ID。|

## 请求示例 {#section_lx1_c25_xfb .section}

``` {#codeblock_8o4_gey_4x0}
https://polardb.aliyuncs.com/?Action=CreateDBCluster
&RegionId=cn-hangzhou
&DBType=MySQL
&DBVersion=5.6
&DBNodeClass=polar.mysql.x2.medium
&PayType=Postpaid
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_l1z_fic_ulu}
<CreateDBClusterResponse>  
    <RequestId>E056BF3D-1E4F-4E39-B729-8491A74B301B</RequestId>
    <OrderId>20235327xxxxx</OrderId>
    <DBClusterId>pc-xxxxxxxxxxxxx</DBClusterId>
</CreateDBClusterResponse>
```

JSON格式

``` {#codeblock_jq4_n7c_78t}
{
  "RequestId": "E056BF3D-1E4F-4E39-B729-8491A74B301B",
  "OrderId": "20235327xxxxx",
  "DBClusterId": "pc-xxxxxxxxxxxxxxx"
}
```

