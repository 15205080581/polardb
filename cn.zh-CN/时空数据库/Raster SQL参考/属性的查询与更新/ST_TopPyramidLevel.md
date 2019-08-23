# ST\_TopPyramidLevel {#reference_r2t_pb4_qfb .reference}

获得raster对象的金字塔最高层级。

## 语法 {#section_ysj_vhn_qfb .section}

```
integer TopPyramidLevel(raster raster_obj);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|raster对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
select ST_TopPyramidLevel(raster_obj) from raster_table;

__________________________________
6
```

