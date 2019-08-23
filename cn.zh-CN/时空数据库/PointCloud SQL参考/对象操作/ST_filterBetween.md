# ST\_filterBetween {#reference_tgy_qxn_qfb .reference}

指定pcpoint某一维度的一大一小两个固定值，过滤出pcpatch中所有该维度值处于两个固定值中间的pcpoint，并以新的pcpatch对象返回。

## 语法 {#section_ysj_vhn_qfb .section}

```
pcpatch ST_filterBetween(pcpatch pc, text dimname, float8 minvalue, float8 maxvalue);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|
|dimname|指定的属性维名称。|
|minvalue|属性固定值最小值。|
|maxvalue|属性固定值最大值。|

## 描述 {#section_yy5_xxn_qfb .section}

返回的结果中，不包括等于一大一小两个固定值的情况。

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_AsText(ST_FilterBetween(pa, 'y', 45.57, 45.60)) FROM patches WHERE id = 7;
------------------------------------------------------------
 {"pcid":1,"pts":[[-126.42,45.58,58,5],[-126.41,45.59,59,5]]}
```

