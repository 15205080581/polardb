# ST\_numPoints {#reference_c4x_vgn_qfb7 .reference}

获取pcpatch对象中的pcpoint个数。

## 语法 {#section_ysj_vhn_qfb .section}

```
integer ST_numPoints(pcpatch pc);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_NumPoints(pa) FROM patches LIMIT 1;
---------------------------
9
```

