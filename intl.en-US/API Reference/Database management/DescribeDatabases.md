# DescribeDatabases {#reference_gng_rdt_xfb .reference}

You can call this operation to query the databases or a specified database of a specified ApsaraDB for POLARDB cluster.

## Description {#section_qbv_kdl_3a2 .section}

If the value types of request parameters are incorrect, the system returns an error response and no data is queried.

## Request parameters {#section_kyn_pgs_xfb .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Set this parameter to DescribeDatabases.|
|DBClusterId|String|Yes|The ID of the ApsaraDB for POLARDB cluster to be queried.|
|DBName|String|No|The name of the database to be queried.|

## Response parameters {#section_cf4_phs_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|<Common response parameters\>|N/A|For more information, see [Common response parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).|
|Databases|List<Database\>|The list of databases.|

## Database {#section_xt3_wdt_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|DBName|String|The name of the database.|
|DBStatus|String|The status of the database. Valid values: -   Creating: The database is being created.
-   Running: The database is being used.
-   Deleting: The database is being deleted.

 |
|DBDescription|String|The description of the database.|
|CharacterSetName|String|The character set of the database. For more information, see [Character sets](intl.en-US/API Reference/Appendixes/Character sets.md#).|
|Accounts|List<Account\>|The list of database accounts.|

## Account {#section_iyx_q2t_xfb .section}

|Parameter|Type|Description|
|:--------|:---|:----------|
|AccountName|String|The name of the database account.|
|AccountStatus|String|The status of the database account. Valid values: -   Creating: The account is being created.
-   Available: The account is available.
-   Deleting: The account is being deleted.

 |
|AccountPrivilege|String|The permissions of the database account on the database.|
|PrivilegeStatus|String|The permission status of the database account. Valid values: -   Empowering: The system is granting permissions to the account.
-   Empowered: Permissions are granted to the account.
-   Removing: The system is revoking permissions for the account.

 |

## Sample request {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeDatabases
&DBClusterId=pc-xxxxxxxxxxxxxxx
&<[Common request parameters]>
```

## Sample response {#section_blw_cls_xfb .section}

XML format

```
<? xml version='1.0' encoding='UTF-8'? >
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

JSON format

```
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

