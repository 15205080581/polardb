# ST\_envelopeAsBinary {#reference_hs4_fb4_qfb .reference}

返回pcpatch对象外包框的wkb值。

## 语法 {#section_ysj_vhn_qfb .section}

```
bytea ST_envelopeAsBinary(pcpatch pc);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|

## 描述 {#section_r5z_jb4_qfb .section}

外包框为ganos geometry的2D geometry对象。

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_EnvelopeAsBinary(pa) FROM patches LIMIT 1;
----------------------------------------------
\x0103000000010000000500000090c2f5285cbf5fc0e17a
14ae4781464090c2f5285cbf5fc0ec51b81e858b46400ad7
a3703dba5fc0ec51b81e858b46400ad7a3703dba5fc0e17a
14ae4781464090c2f5285cbf5fc0e17a14ae47814640
```

