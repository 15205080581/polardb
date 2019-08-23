# S​T\_EraseOverview {#reference_sqn_xc4_qfb .reference}

清空一个raster对象的指定区域。

## 语法 {#section_og1_4hn_qfb .section}

```
raster ST_EraseOverview(raster raster_obj, Box extent, BoxType type,  boolean useNodata);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|raster\_obj|需要操作的影像。|
|extent|需要清空的区域，格式为'\(\(minX,minY\),\(maxX,maxY\)\)'。|
|type|区域的类型，范围的类型，只能是以下一种：Raster（ 影像坐标）、World（世界坐标）。|
|useNodata|是否使用nodata值进行填充。如果指定为false或者未设置nodata值，则使用 0 进行填充。|

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_EraseOverview(raster_obj, '((0,0),(100,100))', 'Raster', false)  from raster_table where id=100;
```

