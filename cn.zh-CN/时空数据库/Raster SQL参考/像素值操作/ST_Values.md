# ST\_Values {#reference_2022069 .reference}

查询Raster对象中与Geometry对象相交的所有像元对应的地理坐标以及像元值。

## 语法 {#section_wkk_wcn_qfb .section}

``` {#codeblock_l94_qyw_bm5}
set of record ST_Values(raster raster_obj,
                     geometry geom,
                     integer pyramidLevel default 0,
                     cstring bands default '',  /* All bands */
                     cstring clipOption default '',
                     out point coords,
                     out integer band,
                     out float8 value)
```

## 参数 {#section_whn_ddn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|需要裁剪的raster对象。|
|pyramidLevel|金字塔层级。|
|geometry|需要裁剪的geometry对象。|
|bands|需要裁剪的波段，用'0-2'或者‘1,2,3’ 这种形式表示，以0开始。 默认为'', 表示裁剪所有的波段。|
|clipOption|json字符串表示的裁剪选项。|
|point|返回结果字段之一，像素值的经纬度（地理）坐标。|
|band|返回结果字段之一，像素值所在波段号。|
|value|返回结果字段之一，像素值。|

clipOption参数如下。

|参数名称|类型|默认值|描述|
|:---|--|---|:-|
|window\_clip|bool|false|是否使用geometry的外包框进行裁剪。取值： -   true：使用geometry的MBR裁剪；
-   false：使用geometry对象裁剪。

 |

## 描述 {#section_f2z_ctn_qfb .section}

-   Geometry对象与Raster对象都需要有空间参考信息，且两者空间参考必须一致。
-   默认的裁剪缓存为100MB，代表最多只能裁剪出100MB大小的结果数据，如果需要调整返回结果大小，可使用参数 ganos.raster.clip\_max\_buffer\_size 调整缓存的大小。

## 示例 {#section_xhh_zfn_qfb .section}

``` {#codeblock_jye_3zz_pbq}
-- 基于点选择
SELECT ( ST_Values(rast, ST_geomfromtext('POINT(128.135 29.774)', 4326)::geometry, 0,'{"window_clip":"true"}')).*
from rat_clip WHERE id=1;
    coord     | band | value 
--------------+------+-------
 (127.8,29.7) |    0 |    11
 (127.8,29.7) |    1 |    10
 (127.8,29.7) |    2 |    50
(3 rows)

-- 基于线选择
SELECT ( ST_Values(rast, ST_geomfromtext('LINESTRING(0 0, 45 45, 90 0, 135 45)', 4326)::geometry, 0)).*
from rat_clip WHERE id=1 limit 10;
    coord    | band | value 
-------------+------+-------
 (44.1,45)   |    0 |   115
 (44.1,45)   |    1 |   112
 (44.1,45)   |    2 |    69
 (45,45)     |    0 |   122
 (45,45)     |    1 |   117
 (45,45)     |    2 |    75
 (134.1,45)  |    0 |    37
 (134.1,45)  |    1 |    64
 (134.1,45)  |    2 |    13
 (43.2,44.1) |    0 |    66
(10 rows)
```

