# ST\_MetaData {#reference_izk_wwn_qfb .reference}

获得raster对象的元数据，返回json格式。

## 语法 {#section_lvh_fxn_qfb .section}

```
text ST_MetaData(raster raster_obj);
```

## 参数 {#section_wzy_jxn_qfb .section}

|参数名称|描述|
|----|--|
|raster\_obj|raster对象。|

## 示例 {#section_lvv_5xn_qfb .section}

```
select ST_MetaData(raster_obj) from raster_table;
```

