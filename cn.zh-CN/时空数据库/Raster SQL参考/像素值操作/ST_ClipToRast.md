# ST\_ClipToRast {#reference_2022040 .reference}

用指定的Geometry对象去裁剪Raster对象，并将裁剪结果作为一个新的Raster对象返回。

## 语法 {#section_wkk_wcn_qfb .section}

``` {#codeblock_l94_qyw_bm5}
raster ST_ClipToRast(raster raster_obj,
                     geometry geom,
                     integer pyramidLevel default 0,
                     cstring bands default '',  /* All bands */
                     float8[] nodata default NULL,
                     cstring clipOption default '',
                     cstring storageOption default '')
```

## 参数 {#section_whn_ddn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|需要裁剪的raster对象。|
|pyramidLevel|金字塔层级。|
|geometry|用于裁剪的geometry对象。|
|bands|需要裁剪的波段，用'0-2'或者‘1,2,3’ 这种形式表示，以0开始。 默认为'', 表示裁剪所有的波段。|
|nodata|用float8\[\]表示的nodata数值。 如果数值个数少于波段数量，则使用波段设置的nodata值填充。如果波段未设置nodata，则用0填充。|
|clipOption|json字符串表示的裁剪选项。|
|storageOption|json字符串表示的返回结果的存储选项。|

clipOption参数如下。

|参数名称|类型|默认值|描述|
|:---|--|---|:-|
|window\_clip|bool|false|是否使用geometry的外包框进行裁剪。取值： -   true：使用geometry的MBR裁剪；
-   false：使用geometry对象裁剪。

 |

storageOption参数如下。

|参数名称|类型|默认值|描述|
|:---|--|---|:-|
|chunking|boolean|和原始raster一致|是否使用分块存储。|
|chunkdim|string|和原始raster一致|分块的维度信息。在chunking=true时才有效。|
|chunktable|string|''|分块表名称。如果传入''值，则会产生一个随机表名临时块表用于存放数据。 该临时表只在当前会话中中有效。如果需要保持一个可访问的裁剪对象，则需要指定块表名称。|
|compression|string|lz4|压缩算法类型。取值： -   none
-   jpeg
-   zlib
-   png
-   lzo
-   lz4

 |
|quality|integer|75|压缩质量，只针对jpeg压缩算法。|
|interleaving|string|和原始raster一致|交错方式。取值： -   bip：Band interleaved by pixel；
-   bil：Band nterleaved by pixel；
-   bsq：Band Sequential。

 |
|endian|string|和原始raster一致|字节序。取值： -   NDR：Little endian；
-   XDR：Big endian。

 |

## 描述 {#section_f2z_ctn_qfb .section}

-   如果chunkTable传入为NULL或者''， 则会产生一个随机表名的临时块表用于存放数据，该临时表只在当前会话中中有效。如果需要保持一个可访问的裁剪对象，则需要指定块表名称。
-   默认的裁剪缓存为100MB，代表最多只能裁剪出100MB大小的结果数据，如果需要调整返回结果大小，可使用参数 ganos.raster.clip\_max\_buffer\_size 设置缓存的大小。

## 示例 {#section_xhh_zfn_qfb .section}

``` {#codeblock_jye_3zz_pbq}
-- 永久表
CREATE TEMP TABLE rast_clip_result(id integer, rast raster);
-- 临时表
CREATE TEMP TABLE rast_clip_result_temp(id integer, rast raster);

-- 默认裁剪并存放到临时表中
INSERT INTO rast_clip_result_temp(id, rast) 
select 1, ST_ClipToRast(rast, ST_geomfromtext('Polygon((0 0, 45 45, 90 45, 45 0, 0 0))', 4326), 0) 
from clip_table 
where id =1；

-- 使用白色作为背景色填充,并保存到永久表中
INSERT INTO rast_clip_result(id, rast) 
select 2, ST_ClipToRast(rast, ST_geomfromtext('Polygon((0 0, 45 45, 90 45, 45 0, 0 0))', 4326), 0, '', ARRAY[254,254,254], '', '{"chunktable":"clip_rbt"}') 
from clip_table 
where id =1;

-- 使用geometry的窗口裁剪
INSERT INTO rast_clip_result_temp(id, rast) 
SELECT 3, ST_ClipToRast(rast, ST_geomfromtext('Polygon((0 0, 45 45, 90 45, 45 0, 0 0))', 4326), 0, '', NULL, '{"window_clip":true}', '') 
from clip_table 
where id =1;
```

