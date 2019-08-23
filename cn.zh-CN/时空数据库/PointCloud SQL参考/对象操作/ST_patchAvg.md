# ST\_patchAvg {#reference_c4x_vgn_qfb .reference}

计算pcpatch对象中所有pcpoint某一属性维度的平均值。

## 语法 {#section_ysj_vhn_qfb .section}

```
numeric ST_patchAvg(pcpatch pc, text dimname);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|
|dimname|指定的属性维名称。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_PatchAvg(pa, 'intensity') FROM patches WHERE id = 7;
--------------------------
5.0000000000000000
```

