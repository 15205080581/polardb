# ST\_isSorted {#reference_qkj_zyn_qfb .reference}

判断pcpatch中所有pcpoint是否按指定的维度进行排序。

## 语法 {#section_ysj_vhn_qfb .section}

```
boolean ST_isSorted(pcpatch pc, text[] dimnames, boolean strict default true);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|
|dimnames|属性维度名称数组。|
|strict|如果为true则进一步要求单个pcpoint的属性维度无重复。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_isSorted(pa, ['y','m']::array) FROM patches;
--------------------------    ----------------------------------
 f
(1 rows)
```

