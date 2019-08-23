# ST\_intersects {#reference_fn3_cc4_qfb .reference}

判断两个pcpatch对象的外包框是否相交。

## 语法 {#section_ysj_vhn_qfb .section}

```
boolean ST_intersects(pcpatch pp1, pcpatch pp2);
boolean ST_intersects(geometry g,  pcpatch pp1);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pp1|pcpatch对象1。|
|pp2|pcpatch对象2。|
|g|ganos geometry的geometry对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
-- Patch should intersect itself
SELECT ST_Intersects(
         '01010000000000000001000000C8CEFFFFF8110000102700000A00'::pcpatch,
         '01010000000000000001000000C8CEFFFFF8110000102700000A00'::pcpatch);
------------------------
t

SELECT ST_Intersects('SRID=4326;POINT(-126.451 45.552)'::geometry, pa) FROM patches WHERE id = 7;
------------------------
t
```

