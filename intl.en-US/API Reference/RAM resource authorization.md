# RAM resource authorization {#concept_263082 .concept}

## Overview {#section_l21_v32_12b .section}

All ApsaraDB for POLARDB clusters created under your Alibaba Cloud account are resources owned by your account. By default, you have full operation permissions on the resources under your account.

Alibaba Cloud Resource Access Management \(RAM\) allows you to grant RAM users the access and management permissions on POLARDB resources owned by your account. For more information, see [RAM authorization](https://www.alibabacloud.com/help/doc-detail/93736.htm).

This topic describes how to grant RAM users the permissions on POLARDB resources.

## Request parameters {#section_qzx_w32_12b .section}

|Resource|Description in an authorization policy|
|--------|--------------------------------------|
|dbcluster| acs:polardb:$regionid:$accountid:dbcluster/

 acs:polardb:\*:\*:dbcluster/

 |

**Parameter description**

|Parameter|Description|
|---------|-----------|
|**$regionid**|The ID of the region, which can be replaced by an asterisk \(\*\).|
|**$accountid**|The ID of your Alibaba Cloud account, which can be replaced by an asterisk \(\*\).|

**Note:** Currently, you are allowed to grant RAM users the permissions on all POLARDB clusters under your account, but not on specific clusters. That is, `acs:polardb:*:*:dbcluster/pc-xxxxxxx` is not supported.

**Example**

``` {#codeblock_d48_mv4_v00}
{
  "Version": "1",
  "Statement": [
    {
      "Action": [
        "polardb:Describe*"
      ],
      "Effect": "Allow",
      "Resource": [
        "acs:polardb:cn-hangzhou:12345678901234:dbcluster/*"
      ]
    },
    {
      "Action": "polardb:Describe*",
      "Effect": "Allow",
      "Resource": [
        "*"
      ]
    }
  ]
}
```

