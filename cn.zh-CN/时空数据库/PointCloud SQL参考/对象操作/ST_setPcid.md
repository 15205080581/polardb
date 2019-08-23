# ST\_setPcid {#reference_u3q_szn_qfb .reference}

给pcpatch对象设置新的schema，返回新的pcpatch。

## 语法 {#section_ysj_vhn_qfb .section}

```
pcpatch ST_setPcid(pcpatch pc, integer pcid, float8 def default 0.0);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|
|pcid|新的schema ID值，来自表pointcloud\_formats。|
|def|指定值，针对在新的schema中存在而在旧的schema中不存在的属性维，设为该指定值，该指定值的默认值是0.0。|

## 描述 {#section_v4p_wzn_qfb .section}

在旧的schema中存在而新的schema中不存在的属性维将被丢弃。

## 示例 {#section_cxp_4jn_qfb .section}

```
update patches set pa=ST_setPcid(pa, 2, 0.0);
--------------------------------------
(1 rows)
```

