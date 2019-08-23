# ST\_SetNoData {#reference_994984 .reference}

设置raster对象的指定波段的NoData（无效值标识）的值。

## 语法 {#section_yw1_w9r_2id .section}

``` {#codeblock_uyl_nxn_fl5}
raster ST_SetNoData(raster rast, integer band_sn, double nodata_value);
```

## 参数 {#section_69x_02w_1jv .section}

|参数名称|描述|
|----|--|
|rast|raster对象。|
|band|指定的波段序号，从0开始，-1表示所有波段。|
|nodata\_value|指定设置的nodata值。|

## 示例 {#section_k1c_k6d_8gn .section}

``` {#codeblock_ucu_jov_gfi}
update rast set rast=ST_SetNoData(rast,0, 999.999);

__________________________________
(1 row)
```

