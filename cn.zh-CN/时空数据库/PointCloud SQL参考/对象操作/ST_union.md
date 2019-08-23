# ST\_union {#reference_c4x_vgn_qfb .reference}

将pcpatch数组聚合成单个pcpatch对象。

## 语法 {#section_ysj_vhn_qfbb .section}

```
pcpatch ST_union(pcpatch[] pcs);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pcs|pcpatch数组。|

## 示例 {#section_cxp_4jn_qfb .section}

```
-- Compare npoints(sum(patches)) to sum(npoints(patches))
SELECT ST_NumPoints(ST_Union(pa)) FROM patches;
SELECT Sum(ST_NumPoints(pa)) FROM patches;

100
```

