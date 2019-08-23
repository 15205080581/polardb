# ST\_Extent {#reference_tyy_4c4_qfb .reference}

获得raster对象的坐标范围，返回PostgreSQL的BOX对象，格式为'\(\(minX,minY\),\(maxX,maxY\)\)'。

## 语法 {#section_ysj_vhn_qfb .section}

``` {#codeblock_4og_9u8_qq5}
BOX ST_Extent(raster raster_obj,CoorSpatialOption csOption = 'WorldFirst')
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|raster对象。|
|CoorSpatialOption|坐标空间选项枚举值。|

## 描述 {#section_l12_wc4_qfb .section}

CoorSpatialOption为坐标空间选项，可取以下值：

-   Raster：影像坐标空间，返回像元坐标；
-   World：世界坐标空间，返回世界坐标；
-   WorldFirst：世界坐标空间优先，即如果已地理参考，则返回世界坐标，如果未地理参考，则返回像元坐标。

## 示例 {#section_cxp_4jn_qfb .section}

``` {#codeblock_9eu_oh2_ys4}
select ST_Extent(raster_obj, 'Raster') from raster_table;

__________________________________
(0 0, 255 255)
```

