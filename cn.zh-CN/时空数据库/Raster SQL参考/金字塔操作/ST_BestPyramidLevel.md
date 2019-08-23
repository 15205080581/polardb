# ST\_BestPyramidLevel {#reference_lpr_zgn_qfb .reference}

根据视口的世界坐标范围，长和宽来计算最佳的金字塔层级。

## 语法 {#section_wkk_wcn_qfb .section}

``` {#codeblock_xf2_fil_fvx}
integer ST_BestPyramidLevel(raster rast, Box extent, integer width, integer height );
```

## 参数 {#section_whn_ddn_qfb .section}

|参数名称|描述|
|:---|:-|
|rast|需要转换的raster对象。|
|box|视口的世界空间坐标范围，格式为`((minX,minY),(maxX,maxY))`。|
|width|视口的像素宽度。|
|height|视口的像素高度。|

## 描述 {#section_6kp_2co_y1s .section}

raster对象必须要有完整的空间参考信息（srid值有效）。

## 示例 {#section_xhh_zfn_qfb .section}

``` {#codeblock_v6i_6yp_7n1}
Select ST_BestPyramidLevel(raster_obj, '((128.0, 30.0),(128.5, 30.5))', 800, 600) from raster_table where id = 10;

---------------------
3
```

