# ST\_CreateRast {#reference_lpr_zgn_qfb .reference}

创建一个基于阿里云对象存储服务（OSS）的raster对象。

## 语法 {#section_wkk_wcn_qfb .section}

``` {#codeblock_0j1_46p_01x}
raster ST_CreateRast(cstring url);
```

## 参数 {#section_whn_ddn_qfb .section}

|参数名称|描述|
|:---|:-|
|url|OSS影像文件的路径。|

## 描述 {#section_f2z_ctn_qfb .section}

oss文件路径格式如下： `oss://access_id:secrect_key@endpoint/path_to/file`。 其中endpoint可以被省略，系统会自动寻找相应的endpoint。如果endpoint被省略，路径必须以/开头。

Endpoint为oss的地域节点。为保证数据导入的性能，请确保云数据库POLARDB与OSS所在Region相同，相关信息请参考[OSS endpoint](https://help.aliyun.com/document_detail/31834.html) 信息。

## 示例 {#section_xhh_zfn_qfb .section}

``` {#codeblock_sd7_y0l_oc6}
-- 基于OSS存储，指定accessID,accessKEY,endpoint
Select ST_CreateRast('OSS://ABCDEFG:1234567890@oss-cn.aliyuncs.com/mybucket/data/4.tif');

-- 基于OSS存储，指定accessID,accessKEY
Select ST_CreateRast('OSS://ABCDEFG:1234567890@/mybucket/data/4.tif');

-- 基于OSS存储，直接指定https形式的URL，该模式性能较差
Select ST_CreateRast('https://mybuckets.oss-cn.aliyuncs.com/data/4.tif');
```

