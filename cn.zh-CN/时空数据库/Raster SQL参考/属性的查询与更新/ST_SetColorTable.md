# ST\_SetColorTable {#reference_994989 .reference}

设置raster对象的指定波段的颜色表信息，采用颜色表的json格式。

## 语法 {#section_6jl_6w2_4xo .section}

``` {#codeblock_zkz_mic_qsj}
raster ST_SetColorTable(raster rast, integer band_sn, cstring clb);
```

## 参数 {#section_5gm_s6f_vlh .section}

|参数名称|描述|
|----|--|
|rast|raster对象。|
|band\_sn|指定的波段序号，从0开始。|
|clb|颜色表的json格式,参考ST\_ColorTable。|

## 示例 {#section_rv5_1sn_zip .section}

``` {#codeblock_6sq_oy6_rbq}
update rast set rast=ST_SetColorTable(rast,0, 
'{"compsCount":4,
    "entries":[
        {"value":0,"c1":0,"c2":0,"c3":0,"c4":255},
        {"value":1,"c1":0,"c2":0,"c3":85,"c4":255},
        {"value":2,"c1":0,"c2":0,"c3":170,"c4":255}
    ]
}');

__________________________________
(1 row)
```

