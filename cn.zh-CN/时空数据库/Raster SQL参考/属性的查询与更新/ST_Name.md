# ST\_Name {#reference_994917 .reference}

获得raster对象的名称。如果没有定义名称，则返回空值。

## 语法 {#section_ay1_jp8_k8c .section}

``` {#codeblock_k6j_890_bpq}
text ST_Name(raster rast);
```

## 参数 {#section_28c_ygv_qhx .section}

|参数名称|描述|
|----|--|
|rast|raster对象。|

## 示例 {#section_h7e_0tf_6v5 .section}

``` {#codeblock_1i6_abf_kad}
select ST_Name(rast) from rat where id=1;

__________________________________
image1
```

