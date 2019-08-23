# DescribeCharacterSetName {#reference_ckv_qft_xfb .reference}

 该接口用于查看数据库字符集信息。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DescribeCharacterSetName。|
|RegionId|String|是|地域ID。|
|DBType|String|否|数据库类型。|
|DBVersion|String|否|数据库版本号。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|
|Engine|String|引擎。|
|CharacterSetNameItems|List<String\>|字符组成的集合。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DescribeCharacterSetName
&RegionId=cn-hangzhou
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<DescribeCharacterSetNameResponse>  
	<CharacterSetNameItems>
		<CharacterSetName>utf8</CharacterSetName>
		<CharacterSetName>gbk</CharacterSetName>
		<CharacterSetName>utf8mb4</CharacterSetName>
		<CharacterSetName>latin1</CharacterSetName>
		<CharacterSetName>euckr</CharacterSetName>
		<CharacterSetName>armscii8</CharacterSetName>
		<CharacterSetName>ascii</CharacterSetName>
		<CharacterSetName>big5</CharacterSetName>
		<CharacterSetName>binary</CharacterSetName>
		<CharacterSetName>cp1250</CharacterSetName>
		<CharacterSetName>cp1251</CharacterSetName>
		<CharacterSetName>cp1256</CharacterSetName>
		<CharacterSetName>cp1257</CharacterSetName>
		<CharacterSetName>cp850</CharacterSetName>
		<CharacterSetName>cp852</CharacterSetName>
		<CharacterSetName>cp866</CharacterSetName>
		<CharacterSetName>cp932</CharacterSetName>
		<CharacterSetName>dec8</CharacterSetName>
		<CharacterSetName>eucjpms</CharacterSetName>
		<CharacterSetName>gb2312</CharacterSetName>
		<CharacterSetName>geostd8</CharacterSetName>
		<CharacterSetName>greek</CharacterSetName>
		<CharacterSetName>hebrew</CharacterSetName>
		<CharacterSetName>hp8</CharacterSetName>
		<CharacterSetName>keybcs2</CharacterSetName>
		<CharacterSetName>koi8r</CharacterSetName>
		<CharacterSetName>koi8u</CharacterSetName>
		<CharacterSetName>latin2</CharacterSetName>
		<CharacterSetName>latin5</CharacterSetName>
		<CharacterSetName>latin7</CharacterSetName>
		<CharacterSetName>macce</CharacterSetName>
		<CharacterSetName>macroman</CharacterSetName>
		<CharacterSetName>sjis</CharacterSetName>
		<CharacterSetName>swe7</CharacterSetName>
		<CharacterSetName>tis620</CharacterSetName>
		<CharacterSetName>ucs2</CharacterSetName>
		<CharacterSetName>ujis</CharacterSetName>
		<CharacterSetName>utf16</CharacterSetName>
		<CharacterSetName>utf16le</CharacterSetName>
		<CharacterSetName>utf32</CharacterSetName>
	</CharacterSetNameItems>
	<RequestId>EF5CAA3B-B7BE-4F8A-B868-8D2C5BB4E104</RequestId>
	<Engine>polardb_mysql</Engine>
</DescribeCharacterSetNameResponse>
```

JSON格式

```
{
    "CharacterSetNameItems":{
        "CharacterSetName":[
            "utf8",
            "gbk",
            "utf8mb4",
            "latin1",
            "euckr",
            "armscii8",
            "ascii",
            "big5",
            "binary",
            "cp1250",
            "cp1251",
            "cp1256",
            "cp1257",
            "cp850",
            "cp852",
            "cp866",
            "cp932",
            "dec8",
            "eucjpms",
            "gb2312",
            "geostd8",
            "greek",
            "hebrew",
            "hp8",
            "keybcs2",
            "koi8r",
            "koi8u",
            "latin2",
            "latin5",
            "latin7",
            "macce",
            "macroman",
            "sjis",
            "swe7",
            "tis620",
            "ucs2",
            "ujis",
            "utf16",
            "utf16le",
            "utf32"
        ]
    },
    "RequestId":"EF5CAA3B-B7BE-4F8A-B868-8D2C5BB4E104",
    "Engine":"polardb_mysql"
}
```

