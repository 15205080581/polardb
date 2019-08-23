# ST\_transform {#reference_ozv_zzn_qfb .reference}

将pcpatch对象转换为新的schema，返回新的pcpatch。

## 语法 {#section_ysj_vhn_qfb .section}

```
pcpatch ST_transform(pcpatch pc, integer pcid, float8 def default 0.0);
```

## 参数 {#section_gyb_phn_qfb .section}

|参数名称|描述|
|:---|:-|
|pc|pcpatch对象。|
|pcid|新的schema ID值，来自表pointcloud\_formats。|
|def|指定值，针对在新的schema中存在而在旧的schema中不存在的属性维，设为该指定值，该指定值的默认值是0.0。|

## 描述 {#section_v4p_wzn_qfb .section}

与st\_setpcid不同的地方是，st\_transform允许将pcpatch的值根据新的schema中维度的重解读、缩放、偏移而进行改变。

## 示例 {#section_cxp_4jn_qfb .section}

```
update patches set pa=ST_transform(pa, 2, 0.0);
--------------------------------------
(1 rows)
```

