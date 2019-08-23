# DeleteDatabase {#reference_psk_fft_xfb .reference}

该接口用于删除POLARDB集群下的数据库。

## 描述 {#section_sxs_fps_xfb .section}

接口必须满足以下条件，否则将删除失败：

-   当前集群状态：运行中；
-   当前集群锁定模式：正常。

## 请求参数 {#section_kyn_pgs_xfb .section}

|名称|类型|是否必须|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：DeleteDatabase。|
|DBClusterId|String|是|集群ID。|
|DBName|String|是|数据库名。|

## 返回参数 {#section_cf4_phs_xfb .section}

|名称|类型|描述|
|:-|:-|:-|
|<公共返回参数\>|-|详见[公共返回参数](intl.zh-CN/API参考/ 使用API/公共参数.md#)。|

## 请求示例 {#section_snj_c3s_xfb .section}

```
https://polardb.aliyuncs.com/?Action=DeleteDatabase
&DBClusterId=pc-xxxxxxxxxx
&DBName=testDB
&<[公共请求参数]>
```

## 返回示例 {#section_blw_cls_xfb .section}

XML格式

```
<DeleteDatabaseResponse>  
     <RequestId>2FED790E-FB61-4721-8C1C-07C627FA5A19</RequestId>
</DeleteDatabaseResponse>
```

JSON格式

```
{
   "RequestId": "2FED790E-FB61-4721-8C1C-07C627FA5A19"
}
```

