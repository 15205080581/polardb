# ST\_UnGeoreference {#reference_994932 .reference}

去掉raster对象的地理参考信息。

## 语法 {#section_clo_vk5_vsj .section}

``` {#codeblock_b83_fgi_umq}
raster ST_UnGeoreference(raster rast);
```

## 参数 {#section_x11_oiv_t7b .section}

|参数名称|描述|
|----|--|
|rast|raster对象。|

## 示例 {#section_akw_8lm_grt .section}

``` {#codeblock_h4a_qp4_ffb}
update rast set rast=ST_UnGeoreference(rast) where id=1;

__________________________________
(1 row)
```

