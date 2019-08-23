# S​T\_ExportTo {#reference_lpr_zgn_qfb .reference}

将一个raster对象导出为OSS文件。

## 语法 {#section_wkk_wcn_qfb .section}

``` {#codeblock_kbi_ewy_5w0}
boolean ST_ExportTo(raster source,  cstring format, cstring url,  integer level = 0);
```

## 参数 {#section_whn_ddn_qfb .section}

|参数名称|描述|
|:---|:-|
|source|需要导出的raster对象。|
|format|导出的数据，常见如 GTiff，BMP 等。|
|url|外部文件路径，参考[ST\_CreateRast](cn.zh-CN/时空数据库/Raster SQL参考/构造函数/ST_CreateRast.md#)中构建路径的描述。|
|level|金字塔级别。|

## 描述 {#section_qns_xtn_qfb .section}

导出成功返回true，失败则返回false。

format指定导出格式的名称，常见格式如下。

|名称|全称|
|--|--|
|BMP|Microsoft Windows Device Independent Bitmap\(.bmp\)|
|ECW|ERDAS Compressed Wavelets \(.ecw\)|
|EHdr|ESRI .hdr Labelled|
|GIF|Graphics InterchangeFormat\(.gif\)|
|GPKG|GeoPackage|
|GTiff|TIFF/BigTIFF/GeoTIFF\(.tif\)|
|HDF4|Hierarchical Data Format Release 4 \(HDF4\)|
|PDF|Geospatial PDF|
|PNG|Portable Network Graphics \(.png\)|

## 示例 {#section_jtq_jvl_sfb .section}

``` {#codeblock_udo_yqp_tru}
Select ST_ExportTo(raster, 'GTiff', 'OSS://ABCDEFG:1234567890@oss-cn.aliyuncs.com/mybucket/data/4.tif') from raster_table where id=1;
```

