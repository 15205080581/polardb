# S​T\_ClipDimension {#reference_lpr_zgn_qfb .reference}

计算Clip结果的像素坐标。

## 语法 {#section_wkk_wcn_qfb .section}

``` {#codeblock_leh_j4o_dkk}
box ST_ClipDimension(raster raster_obj， integer pyramidLevel,  box extent);
```

## 参数 {#section_whn_ddn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|需要转换的raster对象。|
|pyramidLevel|需要转换的金字塔层级。|
|box|需要转换的世界空间坐标。|

## 描述 {#section_f2z_ctn_qfb .section}

raster对象必须要有完整的空间参考信息（srid值有效）。

## 示例 {#section_xhh_zfn_qfb .section}

``` {#codeblock_roh_f5r_4sg}
Select ST_ClipDimension(raster_obj, 2, '((128.0, 30.0),(128.5, 30.5))') from raster_table where id = 10;

------------------------------------
'((200, 300),(600, 720))'
```

