# ST\_range {#reference_xkm_mzn_qfb .reference}

获取pcpatch中从指定序号start开始后的n个pcpoint，返回新的pcpatch。

## 语法 {#section_ysj_vhn_qfb .section}

```
pcpatch ST_range(pcpatch pc, integer start, integer n);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|
|start|指定的pcpoint序号，基数从1开始。|
|n|指定序号（包含自身）往后的pcpoint个数。|

## 示例 {#section_cxp_4jn_qfb .section}

```
update patches set pa=ST_range(pa, 2, 16);
--------------------------------------
(1 rows)
```

