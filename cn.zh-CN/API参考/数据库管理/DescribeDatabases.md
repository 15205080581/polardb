# DescribeDatabases {#reference_gng_rdt_xfb .reference}

该接口用于查询POLARDB指定集群、指定数据库的数据库列表信息。

## 描述 {#section_qbv_kdl_3a2 .section}

如果查询参数类型错误，将返回错误提示，返回数据为空。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeDatabases。|
|DBClusterId|String|是|集群ID。|
|DBName|String|否|数据库名。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](cn.zh-CN/API参考/ 使用API/公共参数.md#)。|
|Databases|List<Database\>|数据库组成的集合。|

## Database参数 {#section_xt3_wdt_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|DBName|String|数据库名。|
|DBStatus|String|数据库状态： -   Creating：创建中；
-   Running：使用中；
-   Deleting：删除中。

 |
|DBDescription|String|数据库备注。|
|CharacterSetName|String|字符集，参见[字符集表](cn.zh-CN/API参考/附表/字符集表.md#)。|
|Accounts|List<Account\>|账号组成的集合。|

## Account参数 {#section_iyx_q2t_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|AccountName|String|账号名。|
|AccountStatus|String|账号状态： -   Creating：创建中；
-   Available：可用；
-   Deleting：删除中。

 |
|AccountPrivilege|String|账号权限。|
|PrivilegeStatus|String|授权状态： -   Empowering：授权中；
-   Empowered：授权完成；
-   Removing：移除权限中。

 |

## 请求示例 {#section_snj_c3s_xfb .section}

``` {#codeblock_pga_0wb_m8b}
https://polardb.aliyuncs.com/?Action=DescribeDatabases
&DBClusterId=pc-xxxxxxxxxxxxxxx
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

``` {#codeblock_qtk_cqi_fui}
<?xml version='1.0' encoding='UTF-8'?>
<DescribeDatabasesResponse>
    <Databases>
        <Database>
            <Accounts>
                <Account>
                    <AccountPrivilege>ReadWrite</AccountPrivilege>
                    <AccountStatus>Available</AccountStatus>
                    <AccountName>test_admin</AccountName>
                    <PrivilegeStatus>Empowered</PrivilegeStatus>
                </Account>
            </Accounts>
            <DBStatus>Running</DBStatus>
            <DBDescription></DBDescription>
            <DBName>test_db_4</DBName>
            <Engine>POLARDB</Engine>
            <CharacterSetName>utf8</CharacterSetName>
        </Database>
    </Databases>
    <RequestId>6A83E8E9-D5C4-45CE-85CD-B0A3B2F21F5E</RequestId>
</DescribeDatabasesResponse>
```

JSON格式

``` {#codeblock_xdm_0cz_gll}
{
  "code": "200",
  "data": {
    "Databases": {
      "Database": [
        {
          "CharacterSetName": "utf8",
          "DBDescription": "",
          "DBName": "test_db_2",
          "DBStatus": "Running",
          "Accounts": {
            "Account": [
              {
                "AccountStatus": "Available",
                "AccountPrivilege": "ReadWrite",
                "PrivilegeStatus": "Empowered",
                "AccountName": "test_a"
              },
              {
                "AccountStatus": "Available",
                "AccountPrivilege": "ReadOnly",
                "PrivilegeStatus": "Empowered",
                "AccountName": "test_acc"
              }
            ]
          },
          "Engine": "POLARDB"
        },
        {
          "CharacterSetName": "utf8mb4",
          "DBDescription": "",
          "DBName": "test_db_5",
          "DBStatus": "Running",
          "Accounts": {
            "Account": [
              {
                "AccountStatus": "Available",
                "AccountPrivilege": "ReadWrite",
                "PrivilegeStatus": "Empowered",
                "AccountName": "test_acc"
              }
            ]
          },
          "Engine": "POLARDB"
        }
      ]
    },
    "RequestId": "EB88083B-AEE7-44B1-9AEB-E76337B1B236"
  },
  "requestId": "EB88083B-AEE7-44B1-9AEB-E76337B1B236",
  "successResponse": true
}
```

