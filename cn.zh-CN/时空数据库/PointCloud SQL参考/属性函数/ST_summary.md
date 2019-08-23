# ST\_summary {#reference_c4x_vgn_qfb8 .reference}

获取pcpatch对象的概要信息。

## 语法 {#section_ysj_vhn_qfb .section}

```
text ST_summary(pcpatch pc);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_Summary(pa) FROM patches LIMIT 1;
-----------------------------------
{"pcid":1, "npts":9, "srid":4326, "compr":"dimensional","dims":[{"pos":0,"name":"X","size":4,"type":"int32_t","compr":"sigbits","stats":{"min":-126.99,"max":-126.91,"avg":-126.95}},{"pos":1,"name":"Y","size":4,"type":"int32_t","compr":"sigbits","stats":{"min":45.01,"max":45.09,"avg":45.05}},{"pos":2,"name":"Z","size":4,"type":"int32_t","compr":"sigbits","stats":{"min":1,"max":9,"avg":5}},{"pos":3,"name":"Intensity","size":2,"type":"uint16_t","compr":"rle","stats":{"min":0,"max":0,"avg":0}}]}
```

