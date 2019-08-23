# ST\_IsGeoreferenced {#reference_hj5_z24_qfb .reference}

获取raster对象是否已被地理参考。boolean格式的返回结果为：“t” 或 “f”。

## 语法 {#section_ysj_vhn_qfb .section}

```
boolean ST_IsGeoreferenced(raster raster_obj);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|raster\_obj|raster对象。|

## 描述 {#section_u1q_pg4_qfb .section}

返回结果t表示true，f表示false。

## 示例 {#section_cxp_4jn_qfb .section}

```
select ST_IsGeoreferenced(raster_obj) from raster_table where id=1;

__________________________________
t
```

