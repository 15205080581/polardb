# ST\_patchMax {#reference_c1b_lwn_qfb .reference}

计算pcpatch对象中所有pcpoint某一属性维度的最大值。

## 语法 {#section_ysj_vhn_qfb .section}

```
numeric ST_patchMax(pcpatch pc, text dimname);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|
|dimname|指定的属性维名称。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_PatchMax(pa, 'intensity') FROM patches WHERE id = 7;
--------------------------
125.0000000000000000
```

