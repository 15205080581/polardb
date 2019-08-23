# ST\_makePatch {#reference_c4x_vgn_qfb .reference}

构造一个pcpatch对象。

## 语法 {#section_ysj_vhn_qfb .section}

```
pcpatch ST_makePatch(integer pcid,  float8[] vals);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pcid|schema的id，来自表point\_cloud\_formats。|
|float8\[\]|float8数组，数组元素为schema的dimension维度数的整数倍。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_asText(ST_MakePatch(1, ARRAY[-126.99,45.01,1,0, -126.98,45.02,2,0, -126.97,45.03,3,0]));
-------------------------------------------------
{"pcid":1,"pts":[
 [-126.99,45.01,1,0],[-126.98,45.02,2,0],[-126.97,45.03,3,0]
]}
```

