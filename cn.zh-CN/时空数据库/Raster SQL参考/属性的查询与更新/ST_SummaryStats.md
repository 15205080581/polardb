# ST\_SummaryStats {#reference_f3p_gf4_qfb .reference}

计算一个raster对象的指定波段集的统计值信息。

## 语法 {#section_og1_4hn_qfb .section}

```
raster ST_SummaryStats(raster raster_obj) ;
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|raster\_obj|Raster对象。|

## 示例 {#section_lmw_qhn_qfb .section}

```
update raster_obj set raster_obj=ST_SummaryStats(raster_obj) where id = 1;
__________________________________
(1 row)
```

