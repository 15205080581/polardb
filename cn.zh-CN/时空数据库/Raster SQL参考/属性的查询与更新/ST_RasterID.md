# ST\_RasterID {#reference_wtr_114_qfb .reference}

获得raster对象的UUID（通用唯一识别码）。

## 语法 {#section_ysj_vhn_qfb .section}

```
text ST_RasterID(raster raster_obj);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|raster对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
select ST_RasterID(raster_obj) from raster_table;

——————————————————————————————————
4e692ed0-74e2-42a3-a10d-c28d4ae31982
```

