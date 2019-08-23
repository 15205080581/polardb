# ST\_intersection {#reference_q3x_sb4_qfb .reference}

将pcpatch对象和给定的几何对象进行相交处理，返回相交处理后的子pcpatch对象。

## 语法 {#section_ysj_vhn_qfb .section}

```
pcpatch ST_intersection(pcpatch pc, geometry geom);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|
|geom|ganos geometry的geometry对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_AsText(ST_Explode(ST_Intersection(
      pa,
      'SRID=4326;POLYGON((-126.451 45.552, -126.42 47.55, -126.40 45.552, -126.451 45.552))'::geometry
)))
FROM patches WHERE id = 7;

             st_astext
--------------------------------------
 {"pcid":1,"pt":[-126.44,45.56,56,5]}
 {"pcid":1,"pt":[-126.43,45.57,57,5]}
 {"pcid":1,"pt":[-126.42,45.58,58,5]}
 {"pcid":1,"pt":[-126.41,45.59,59,5]}
```

