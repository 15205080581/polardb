# ST\_Width {#reference_jqc_cyn_qfb .reference}

获得raster对象的宽度。如果需要获得分块的宽度，参见ST\_ChuckWidth。

## 语法 {#section_jjm_myn_qfb .section}

```
integer ST_Width(raster raster_obj);
```

## **参数** {#section_syp_pyn_qfb .section}

|参数名称|描述|
|----|--|
|raster\_obj|raster对象。|

## 示例 {#section_gqv_5yn_qfb .section}

```
select ST_Width(raster_obj) from raster_table;

——————————————————————————————
10060
```

