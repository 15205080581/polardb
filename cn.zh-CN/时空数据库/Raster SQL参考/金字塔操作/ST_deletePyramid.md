# ST\_deletePyramid {#concept_978492 .concept}

删除影像金字塔。

## 语法 {#section_qyt_rp8_1d9 .section}

``` {#codeblock_g1j_0w0_9gr}
raster ST_deletePyramid(raster source);
```

## 参数 {#section_dxd_0ga_s0i .section}

|参数名称|描述|
|----|--|
|source|需要删除金字塔的raster对象。|

## 描述 {#section_ttl_75d_4pa .section}

删除影像金字塔，重置影像元数据，删除金字塔块数据。

## 示例 {#section_tb0_vk6_4pm .section}

``` {#codeblock_lvl_5oe_hep}
Update raster_table set raster_obj = ST_deletePyram id(raster_obj) where id = 1;
```

