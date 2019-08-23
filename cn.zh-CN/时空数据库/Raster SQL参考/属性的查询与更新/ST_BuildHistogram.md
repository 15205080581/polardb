# ST\_BuildHistogram {#reference_ytp_kf4_qfb .reference}

计算一个raster对象的指定波段集的直方图信息。

## 语法 {#section_og1_4hn_qfb .section}

```
raster ST_BuildHistogram(raster raster_obj);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|raster\_obj|Raster对象。|

## 示例 {#section_lmw_qhn_qfb .section}

```
UPDATE raster_table SET raster_obj = st_buildhistogram(raster_obj) WHERE id = 1;
--------------------------------
(1 row)
```

