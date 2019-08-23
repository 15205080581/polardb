# ST\_NoData {#reference_wbn_cf4_qfb .reference}

获取raster对象的某一个波段NoData（无效值标识）的值。如果没有NODATA定义，则返回空值。

## 语法 {#section_ysj_vhn_qfb .section}

```
float8 ST_NoData(raster raster_obj, integer band);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|raster对象。|
|band|波段序号，从0开始。|

## 示例 {#section_cxp_4jn_qfb .section}

```
select ST_NoData(raster_obj, 0) from raster_table where id=1;

__________________________________
0.000
```

