# ST\_asBinary {#reference_l35_514_qfb .reference}

返回pcpoint对象的wkb值。

## 语法 {#section_ysj_vhn_qfb .section}

```
bytea ST_asBinary(pcpoint pt);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pt|pcpoint对象。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_AsBinary('010100000064CEFFFF94110000703000000400'::pcpoint);
---------------------------------------------
\x01010000800000000000c05fc000000000008046400000000000005f40
```

