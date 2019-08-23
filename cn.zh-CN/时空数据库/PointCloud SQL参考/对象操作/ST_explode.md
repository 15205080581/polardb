# ST\_explode {#reference_c4x_vgn_qfb .reference}

将pcpatch对象反解为多行的pcpoint。

## 语法 {#section_ysj_vhn_qfbc .section}

```
setof[pcpoint] ST_union(pcpatch pc);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_AsText(ST_Explode(pa)), id FROM patches WHERE id = 7;
-------------------------------------------
              st_astext               | id
--------------------------------------+----
 {"pcid":1,"pt":[-126.5,45.5,50,5]}   |  7
 {"pcid":1,"pt":[-126.49,45.51,51,5]} |  7
 {"pcid":1,"pt":[-126.48,45.52,52,5]} |  7
 {"pcid":1,"pt":[-126.47,45.53,53,5]} |  7
 {"pcid":1,"pt":[-126.46,45.54,54,5]} |  7
 {"pcid":1,"pt":[-126.45,45.55,55,5]} |  7
 {"pcid":1,"pt":[-126.44,45.56,56,5]} |  7
 {"pcid":1,"pt":[-126.43,45.57,57,5]} |  7
 {"pcid":1,"pt":[-126.42,45.58,58,5]} |  7
 {"pcid":1,"pt":[-126.41,45.59,59,5]} |  7
```

