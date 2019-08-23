# ST\_Value {#reference_994922 .reference}

输出指定波段和行列号的像元值。

## 语法 {#section_q81_6qz_1rm .section}

``` {#codeblock_cf5_jdi_52x}
float8 ST_Value(raster rast, integer band, integer colsn, integer rowsn, boolean exclude_nodata_value);
```

## 参数 {#section_jb6_8vr_cnq .section}

|参数名称|描述|
|----|--|
|rast|raster对象。|
|band|波段序号。|
|colsn|像元列号。|
|rowsn|像元行号。|
|exclude\_nodata\_value|是否排除nodata，默认值为true。|

## 描述 {#section_hef_jdr_cyn .section}

输出指定波段和行列号的像元值（波段索引号从0开始），波段号和行列号默认为0。

## 示例 {#section_3pl_9w3_gjy .section}

``` {#codeblock_fkr_yfg_jy4}
select st_value(rast, 1, 3, 4) from t_pixel where id=2;
 st_value 
----------
       88
(1 row)
```

