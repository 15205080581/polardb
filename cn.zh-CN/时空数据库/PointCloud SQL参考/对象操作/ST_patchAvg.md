# ST\_patchAvg {#reference_c4x_vgn_qfb .reference}

计算pcpatch对象中pcpoint所有属性的平均值，返回新的pcpoint对象。

## 语法 {#section_ysj_vhn_qfbd .section}

```
pcpoint ST_patchAvg(pcpatch pc);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_AsText(ST_PatchAvg(pa)) FROM patches WHERE id = 7;
-------------------------------------
{"pcid":1,"pt":[-126.46,45.54,54.5,5]}
```

