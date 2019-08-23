# ST\_Flow\_direction {#reference_978565 .reference}

根据区域中的DEM高程值，计算区域中的水流方向。

## 语法 {#section_4ee_422_uyi .section}

``` {#codeblock_46i_ia9_k1e}
float8[] ST_flow_direction(raster rast, Box box);
```

## 参数 {#section_8ox_pm4_5dn .section}

|参数名称|描述|
|----|--|
|rast|raster对象，目前仅支持1波段的DEM。|
|box|分析区域，世界坐标。|

## 描述 {#section_g3d_9ap_o74 .section}

使用d8算法，根据区域中的DEM高程值，计算区域中的水流方向。

raster对象目前仅支持1波段的DEM数据。

## 示例 {#section_0me_vem_cdm .section}

``` {#codeblock_tkx_n9x_fx6}
select st_flow_direction(rast, '((-202286.94,2232375.16),(-202135.0,2232225))'::box, 1000::float8) from t_overflow where id =2;
                               st_flow_direction                                
--------------------------------------------------------------------------------
 {2,2,2,4,4,8,2,2,2,4,4,8,1,1,2,4,8,4,128,128,1,2,4,8,2,2,1,4,4,4,1,1,1,1,4,16}
(1 row)
```

