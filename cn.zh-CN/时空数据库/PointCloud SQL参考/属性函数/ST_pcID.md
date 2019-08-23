# ST\_pcID {#reference_c4x_vgn_qfb5 .reference}

获取pcpoint/pcpatch对象的schema ID。

## 语法 {#section_ysj_vhn_qfb .section}

```
integer ST_pcID(pcpoint pt);
integer ST_pcID(pcpatch pp)；
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pt|pcpoint对象。|
|pp|pcpatch对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_pcID('010100000064CEFFFF94110000703000000400'::pcpoint);
-------------------------------
1
```

