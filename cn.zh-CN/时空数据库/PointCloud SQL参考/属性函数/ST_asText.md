# ST\_asText {#reference_c4x_vgn_qfb .reference}

将pcpoint/pcpatch对象转为json字符串表达。

## 语法 {#section_ysj_vhn_qfb .section}

```
text ST_asText(pcpatch pp);
text ST_asText(pcpoint pt);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pp|pcpatch对象。|
|pt|pcpoint对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_asText('010100000064CEFFFF94110000703000000400'::pcpoint);
-------------------------------
{"pcid":1,"pt":[-127,45,124,4]}
```

