# ST\_SetName {#reference_994921 .reference}

设置raster对象的名称。

## 语法 {#section_rej_upy_39h .section}

``` {#codeblock_ckc_fs8_y6b}
raster ST_SetName(raster rast, cstring name);
```

## 参数 {#section_i66_4zj_b5s .section}

|参数名称|描述|
|----|--|
|rast|raster对象。|
|name|新的对象名称。|

## 示例 {#section_j81_xl6_jvz .section}

``` {#codeblock_ewm_4bn_eo3}
update rat set rast = ST_SetNam e(rast,'im age2') where id = 2;
——————————————————————————————————
(1 row)
```

