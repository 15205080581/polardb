# ST\_Patch {#reference_c4x_vgn_qfb .reference}

通过pcpoint数组构造一个pcpatch对象。

## 语法 {#section_ysj_vhn_qfb .section}

```
pcpatch ST_Patch(pcpoint[]  pts);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pts|pcpoint数组。|

## 示例 {#section_cxp_4jn_qfb .section}

```
INSERT INTO patches (pa)
SELECT ST_Patch(pt) FROM points GROUP BY id/10;
```

