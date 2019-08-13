# RAM资源授权 {#concept_263082 .concept}

## 描述 {#section_l21_v32_12b .section}

您通过云账号创建的POLARDB集群，都是该账号自己拥有的资源。默认情况下，账号对自己的资源拥有完整的操作权限。

通过使用阿里云的RAM（Resource Access Management）服务，您可以将您云账号下POLARDB资源的访问及管理权限授予RAM中的子用户，详情请参见[RAM授权](https://help.aliyun.com/document_detail/93736.html)。

POLARDB在通过RAM进行授权时，资源的描述方式如下：

## 请求参数 {#section_qzx_w32_12b .section}

|资源类型|授权策略中的资源描述方式|
|----|------------|
|dbcluster| acs:polardb:$regionid:$accountid:dbcluster/

 acs:polardb:\*:\*:dbcluster/

 |

**参数说明：**

|参数名称|说明|
|----|--|
|**$regionid**|地域ID，可以用\*代替。|
|**$accountid**|云账号的数字ID，可以用\*代替。|

**说明：** POLARDB仅支持针对账号下所有集群授权，不支持集群级别的授权，即不支持`acs:polardb:*:*:dbcluster/pc-xxxxxxx`。

**示例**

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

