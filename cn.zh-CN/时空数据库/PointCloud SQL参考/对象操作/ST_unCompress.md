# ST\_unCompress {#reference_c4x_vgn_qfb .reference}

将pcpatch对象解压。

## 语法 {#section_ysj_vhn_qfba .section}

```
pcpatch ST_unCompress(pcpatch pc);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|

## 描述 {#section_wcp_lsn_qfb .section}

所有返回pcpatch对象的接口，在返回pcpatch前都是先按schema中指定的压缩方法进行了压缩。

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_Uncompress(pa) FROM patches  WHERE ST_NumPoints(pa) = 1;
--------------------------------------
01010000000000000001000000C8CEFFFFF8110000102700000A00
```

