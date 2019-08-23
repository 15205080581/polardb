# ST\_boundingDiagonalGeometry {#reference_o5h_n14_qfb .reference}

返回pcpatch对象外包框对角线geometry。

## 语法 {#section_ysj_vhn_qfb .section}

```
geometry ST_boundingDiagonalAsBinary(pcpatch pc);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|

## 描述 {#section_v4p_wzn_qfb .section}

外包框对角线为ganos geometry的2D LineString对象。本函数可用在pcpatch列建索引。

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_AsText(ST_BoundingDiagonalGeometry(pa)) FROM patches;
                  st_astext
------------------------------------------------
LINESTRING Z (-126.99 45.01 1,-126.91 45.09 9)
LINESTRING Z (-126 46 100,-126 46 100)
LINESTRING Z (-126.2 45.8 80,-126.11 45.89 89)
LINESTRING Z (-126.4 45.6 60,-126.31 45.69 69)
LINESTRING Z (-126.3 45.7 70,-126.21 45.79 79)
LINESTRING Z (-126.8 45.2 20,-126.71 45.29 29)
LINESTRING Z (-126.5 45.5 50,-126.41 45.59 59)
LINESTRING Z (-126.6 45.4 40,-126.51 45.49 49)
LINESTRING Z (-126.9 45.1 10,-126.81 45.19 19)
LINESTRING Z (-126.7 45.3 30,-126.61 45.39 39)
LINESTRING Z (-126.1 45.9 90,-126.01 45.99 99)


CREATE INDEX ON patches USING GIST(ST_BoundingDiagonalGeometry(patch) gist_geometry_ops_nd);
```

