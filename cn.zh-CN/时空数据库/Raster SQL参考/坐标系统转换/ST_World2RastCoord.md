# S​T\_World2RastCoord {#reference_lpr_zgn_qfb .reference}

由世界坐标及像元所在金字塔层级，根据逆仿射变换公式计算像元坐标。

## 语法 {#section_wkk_wcn_qfb .section}

``` {#codeblock_j63_vm4_5dr}
point ST_World2RastCoord(raster raster_obj， integer pyramidLevel, point coord);
```

## 参数 {#section_whn_ddn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|需要转换的raster对象。|
|pyramidLevel|需要转换的金字塔层级。|
|coord|需要转换的世界空间坐标。|

## 描述 {#section_f2z_ctn_qfb .section}

raster对象必须要有完整的空间参考信息（srid值有效）。

## 示例 {#section_xhh_zfn_qfb .section}

``` {#codeblock_85h_fbd_8hj}
Select ST_World2RastCoord(raster_obj, 0, '(27.9,128.6)') from raster_table;
```

