# S​T\_MosaicFrom {#reference_lpr_zgn_qfb .reference}

将指定的raster对象进行镶嵌操作，合并成为一个新的raster对象。

## 语法 {#section_wkk_wcn_qfb .section}

```
raster ST_MosaicFrom(raster source[],  cstring chunkTableName);
```

## 参数 {#section_whn_ddn_qfb .section}

|参数名称|描述|
|:---|:-|
|source|需要拼接的源raster对象。|
|chunkTableName|拼接完成的块表名称，必须符合数据库表名规范。|

## 描述 {#section_f2z_ctn_qfb .section}

镶嵌函数会创建一个新的raster对象。

所有指定的raster对象需要满足以下条件：

-   具有相同的波段数。
-   所有的raster对象要么都进行了地理参考，要么都不是。如果都是地理参考，则采用世界坐标镶嵌。
-   指定raster对象的像素类型可以不同。如果是世界坐标镶嵌，则SRID、仿射参数必须一致。

## 示例 {#section_xhh_zfn_qfb .section}

```
Insert Into raster_obj Values(1, ST_MosaicFrom(Array(select raster_obj from raster_table where id < 10), 'chunk_table_mosaic'))
Update raster_table Set raster_obj = ST_MosaicFrom(Array(select raster_obj from raster_table where id < 10), 'chunk_table_mosaic') where id = 11;
```

