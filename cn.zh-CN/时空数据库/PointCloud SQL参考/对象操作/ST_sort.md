# ST\_sort {#reference_fhr_hzn_qfb .reference}

将pcpatch中所有pcpoint按指定的维度进行排序，返回新的pcpatch。

## 语法 {#section_ysj_vhn_qfb .section}

```
pcpatch ST_sort(pcpatch pc, text[] dimnames);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|
|dimnames|属性维度名称数组。|

## 示例 {#section_cxp_4jn_qfb .section}

```
update patches set pa=ST_Sort(pa, ['y','m']::array);
--------------------------------------
(1 rows)
```

