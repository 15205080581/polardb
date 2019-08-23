# ST\_get {#reference_c4x_vgn_qfb .reference}

获取pcpoint对象属性值。

## 语法 {#section_ysj_vhn_qfb .section}

```
float8[]  ST_get(pcpoint pc);
numeric ST_get(pcpoint pc, text dimname);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpoint对象。|
|dimname|指定的属性维度名称。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_Get('010100000064CEFFFF94110000703000000400'::pcpoint, 'Intensity');
-------------------
4

SELECT ST_Get('010100000064CEFFFF94110000703000000400'::pcpoint);
--------------------
{-127,45,124,4}
```

