# ST\_makePoint {#reference_c4x_vgn_qfb1 .reference}

构造一个pcpoint对象。

## 语法 {#section_ysj_vhn_qfb .section}

```
pcpoint ST_makePoint(integer pcid, float8[] vals);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pcid|schema的id，来自表point\_cloud\_formats。|
|float8\[\]|float8数组，数组元素个数取决于schema的dimension。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_makePoint(1, ARRAY[-127, 45, 124.0, 4.0]);
-------------------------------------------------
010100000064CEFFFF94110000703000000400
```

