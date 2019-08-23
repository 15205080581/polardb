# ST\_envelopeGeometry {#reference_l51_h14_qfb .reference}

返回pcpatch对象外包框geometry。

## 语法 {#section_ysj_vhn_qfb .section}

```
geometry ST_envelopeGeometry(pcpatch pc);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|

## 描述 {#section_v4p_wzn_qfb .section}

外包框为ganos geometry的2D geometry对象。

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_AsText(ST_EnvelopeGeometry(pa)) FROM patches LIMIT 1;
------------------------------
POLYGON((-126.99 45.01,-126.99 45.09,-126.91 45.09,-126.91 45.01,-126.99 45.01))

CREATE INDEX ON patches USING GIST(ST_EnvelopeGeometry(patch));
```

