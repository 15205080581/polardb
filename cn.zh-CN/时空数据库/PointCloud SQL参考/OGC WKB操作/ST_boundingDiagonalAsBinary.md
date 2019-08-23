# ST\_boundingDiagonalAsBinary {#reference_mlq_mb4_qfb .reference}

返回pcpatch对象外包框对角线的wkb值。

## 语法 {#section_ysj_vhn_qfb .section}

```
bytea ST_boundingDiagonalAsBinary(pcpatch pc);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|

## 描述 {#section_r5z_jb4_qfb .section}

外包框为2D geometry。

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_BoundingDiagonalAsBinary( ST_Patch(ARRAY[ ST_MakePoint(1, ARRAY[0.,0.,0.,10.]), ST_MakePoint(1, ARRAY[1.,1.,1.,10.]), ST_MakePoint(1, ARRAY[10.,10.,10.,10.])]));
--------------------------------------------------------
\x01020000a0e610000002000000000000000000000000000000000000000000000000000000000000000000244000000000000024400000000000002440
```

