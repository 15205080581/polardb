# ST\_CellType {#reference_kbd_514_qfb .reference}

获得raster对象的像素类型。类型值可以为以下值之一："8BSI"， "8BUI"， "16BSI"， "16BUI"， "32BSI"， "32BUI"， "32BF"， "64BF"。

## 语法 {#section_ysj_vhn_qfb .section}

```
text ST_CellType(raster raster_obj);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|raster对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
select st_celltype(raster_obj) from raster_table;

__________________________________
8BUI
```

