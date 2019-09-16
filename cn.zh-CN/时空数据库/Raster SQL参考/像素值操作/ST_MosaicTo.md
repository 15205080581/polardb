# S​T\_MosaicTo {#reference_lpr_zgn_qfb .reference}

将raster对象或对象集镶嵌到目标raster对象

## 语法 {#section_wkk_wcn_qfb .section}

``` {#codeblock_kdi_6qj_bj7}
raster ST_MosaicTo(raster raster_obj,raster source[]);
```

## 参数 {#section_whn_ddn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|目标raster对象。|
|source|源raster对象或对象集。|

## 描述 {#section_f2z_ctn_qfb .section}

源raster对象和目标raster对象需要满足以下条件：

-   具有相同的波段数。
-   所有的raster对象要么都进行了地理参考，要么都不是。如果都是地理参考，则采用世界坐标镶嵌。
-   指定raster对象的像素类型可以不同。如果是世界坐标镶嵌，则SRID、仿射参数必须一致。

## 示例 {#section_xhh_zfn_qfb .section}

``` {#codeblock_irs_1sd_ndo}
Update raster_table Set raster_obj = ST_MosaicTo(raster_obj, Array(select raster_obj from raster_table where id < 10)) where id = 11;
```

