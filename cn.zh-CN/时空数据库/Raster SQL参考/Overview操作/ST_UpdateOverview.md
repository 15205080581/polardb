# S​T\_UpdateOverview {#reference_p3y_wc4_qfb .reference}

使用raster对象或对象集更新overview。

## 语法 {#section_og1_4hn_qfb .section}

``` {#codeblock_0uh_ob6_0ny}
raster ST_UpdateOverview(raster raster_obj,raster source[]);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|raster\_obj|目标raster对象。|
|source|源raster对象或对象集。|

## 描述 {#section_lkb_rtd_5gb .section}

所有指定的raster对象需要满足以下条件：

-   具有相同的波段数。
-   所有的raster对象都有地理参考坐标，或者都没有，不允许存在部分有部分没有地理参考坐标的情况。如果都有地理参考坐标，则采用世界坐标（地理坐标）镶嵌。
-   指定raster对象的像素类型可以不同。如果是世界坐标镶嵌，则SRID、像素分辨率必须一致。

## 示例 {#section_lmw_qhn_qfb .section}

``` {#codeblock_po3_j8x_s5v}
Update raster_table set raster_obj = ST_UpdateOverview(raster_obj, Array(select raster_obj from raster_table_new)) where id = 1;
```

