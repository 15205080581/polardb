# ST\_pointN {#reference_glj_qyn_qfb .reference}

返回pcpatch中指定序号的pcpoint对象。

## 语法 {#section_ysj_vhn_qfb .section}

```
pcpoint ST_pointN(pcpatch pc, integer n);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|
|n|指定的序号，从1开始，如果是负数，则从pcpatch的末尾开始往前推算|n|。例如n=-2，则从pacpatch的末尾往前推算2位。|

## 示例 {#section_cxp_4jn_qfb .section}

```
SELECT ST_asText(ST_pointN(pa, 4)) FROM patches WHERE id = 7;
----------------------------------
{"pcid":1,"pt":[-126.41,45.59,59,5]}
```

