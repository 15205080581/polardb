# ST\_compress {#reference_c4x_vgn_qfb .reference}

将pcpatch对象按指定方式压缩。

## 语法 {#section_ysj_vhn_qfb9 .section}

```
pcpatch ST_compress(pcpatch pc, text global_compression_schema default '', text compression_config default '');
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|
|global\_compression\_schema|压缩框架。|
|compression\_config|压缩配置项，指定具体维度的压缩算法。|

## 描述 {#section_wcp_lsn_qfb .section}

压缩框架可以为：

```
auto           -- determined by pcid
dimension 
laz             -- no compression config supported
ght            -- is discarded
```

当压缩框架为dimension时，压缩配置项可以为：

```
auto -- determined automatically, from values stats
zlib -- deflate compression
sigbits -- significant bits removal
rle -- run-length encoding
```

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_asText(ST_Compress(ST_MakePatch(1, ARRAY[-126.99,45.01,1,0, -126.98,45.02,2,0, -126.97,45.03,3,0])));

-------------------------------------------------
{"pcid":1,"pts":[
 [-126.99,45.01,1,0],[-126.98,45.02,2,0],[-126.97,45.03,3,0]
]}
```

