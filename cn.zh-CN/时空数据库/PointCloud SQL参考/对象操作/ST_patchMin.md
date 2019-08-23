# ST\_patchMin {#reference_zbl_twn_qfb .reference}

计算pcpatch对象中所有pcpoint某一属性维度的最小值。

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
SELECT ST_PatchMin(pa, 'intensity') FROM patches WHERE id = 7;
--------------------------
0.25122
```

