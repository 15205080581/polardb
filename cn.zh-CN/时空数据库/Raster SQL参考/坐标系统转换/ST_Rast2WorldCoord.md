# S​T\_Rast2WorldCoord {#reference_lpr_zgn_qfb .reference}

由像元坐标及像元所在金字塔层级，根据仿射变换公式计算世界坐标。

## 语法 {#section_wkk_wcn_qfb .section}

``` {#codeblock_rhg_0hs_yxw}
point ST_Rast2WorldCoord(raster raster_obj, integer pyramidLevel,  integer row, integer column);
```

## 参数 {#section_whn_ddn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|目标raster对象|
|pyramidLevel|金字塔层级|
|row|行号|
|column|列号|

## 描述 {#section_f2z_ctn_qfb .section}

raster对象必须要有完整的空间参考信息（srid值有效）。

## 示例 {#section_xhh_zfn_qfb .section}

``` {#codeblock_8fh_kfz_qqn}
Select ST_Rast2WorldCoord(raster_obj, 0, 0, 0) from raster_table;
```

