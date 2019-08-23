# S​T\_BuildPyramid {#reference_lpr_zgn_qfb .reference}

创建影像金字塔。

## 语法 {#section_wkk_wcn_qfb .section}

``` {#codeblock_xon_rta_dxi}
raster ST_BuildPyramid(raster source);
raster ST_BuildPyramid(raster source,  cstring chunkTableName);
```

## 参数 {#section_whn_ddn_qfb .section}

|参数名称|描述|
|:---|:-|
|source|需要创建金字塔的raster对象。|
|chunkTableName|金字塔所存储的分块表名称。|

## 描述 {#section_m04_zuu_n4l .section}

创建金字塔支持GPU加速，如果运行环境带有GPU设备，则Ganos会自动开启GPU加速功能。

## 示例 {#section_xhh_zfn_qfb .section}

``` {#codeblock_wi6_wxa_n0r}
Update raster_table set raster_obj = ST_BuildPyramid(raster_obj) where id = 1;

Update raster_table set raster_obj = ST_BuildPyramid(raster_obj, 'chunk_table') where id = 2;
```

