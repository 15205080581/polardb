# ST\_SetStatistics {#reference_994997 .reference}

设置raster对象的指定波段的统计值信息。

## 语法 {#section_adg_a5i_7ih .section}

``` {#codeblock_2t2_pfg_hu3}
raster ST_SetStatistics(raster rast, integer band, double min, double max, double mean, double std,cstring samplingParams);
```

## 参数 {#section_pbr_6rd_l8u .section}

|参数名称|描述|
|----|--|
|rast|raster对象。|
|band|指定的波段序号，从0开始。|
|min,max,mean,std|统计值。|
|samplingParams|'approx=false' 或者 'appro x=true'。|

## 示例 {#section_f0n_zlh_kc2 .section}

``` {#codeblock_1ui_5my_kzt}
update rast set rast=ST_SetStatistics(rast,0,0.0 , 255.0, 125.0, 23.6, 'approx=false');

__________________________________
(1 row)
```

