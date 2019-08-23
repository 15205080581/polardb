# ST\_CellDepth {#reference_d3l_k14_qfb .reference}

获得raster对象的像素深度。深度值可以为以下值之一：0，1，2，4，8，16，32，64。其中，0为像素深度未知。

## 语法 {#section_ysj_vhn_qfb .section}

```
integer ST_CellDepth(raster raster_obj);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|raster对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
select ST_CellDepth(raster_obj) from raster_table;

__________________________________
8
```

