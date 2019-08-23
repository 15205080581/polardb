# ST\_Clip {#reference_lpr_zgn_qfb .reference}

对raster对象进行裁剪操作。

## 语法 {#section_wkk_wcn_qfb .section}

```
bytea ST_Clip(raster raster_obj,integer pyramidLevel,  box extent, BoxType boxType);
bytea ST_Clip(raster raster_obj,integer pyramidLevel,  box extent, BoxType boxType, integer destSrid);
```

## 参数 {#section_whn_ddn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|需要裁剪的raster对象。|
|pyramidLevel|金字塔层级。|
|extent|需要裁剪的范围，格式为'\(\(minX,minY\),\(maxX,maxY\)\)'。|
|boxType|范围的类型，只能是以下一种：-   Raster （像元坐标）
-   World （世界坐标）

|
|destSrid|指定的输出像元子集的空间参考值。|

## 描述 {#section_f2z_ctn_qfb .section}

ST\_Clip函数返回基于传入窗口大小的像元矩阵，大小不能超过100MB。

## 示例 {#section_xhh_zfn_qfb .section}

```
Select ST_Clip(raster_obj, 0, '((128.980,30.0),(129.0,30.2))', 'World');
Select ST_Clip(raster_obj, 0, '((128.980,30.0),(129.0,30.2))', 'World'， 4326);
```

