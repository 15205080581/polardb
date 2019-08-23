# ST\_ColorInterp {#reference_c12_3f4_qfb .reference}

获取raster对象的某一个波段的颜色解释类型。

## 语法 {#section_og1_4hn_qfb .section}

``` {#codeblock_gi4_spn_rm0}
text ST_ColorInterp(raster raster_obj, integer band);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|raster\_obj|Raster对象。|
|band|波段序号，从0开始。|

返回的interp值及其说明如下表。

|值|说明|
|--|--|
|Undefined|颜色解释类型未定义。|
|GrayIndex|灰度值索引。|
|PaletteIndex|颜色表索引。|
|RedBand|RGB颜色模型Red波段。|
|GreenBand|RGB颜色模型Green波段。|
|BlueBand|RGB颜色模型Blue波段。|
|AlphaBand|RGBA颜色模型Alpha波段。|
|HueBand|HSL颜色模型中Hue波段。|
|SaturationBand|HSL颜色模型中Saturation波段。|
|LightnessBand|HSL颜色模型中Lightness波段。|
|CyanBand|CMYK颜色模型中Cyan波段。|
|MagentaBand|CMYK颜色模型中Magenta波段。|
|YellowBand|CMYK颜色模型中Yellow波段。|
|BlackBand|CMYK颜色模型中Black波段。|
|YCbCr\_YBand|YCBCR颜色模型中Y波段。|
|YCbCr\_CbBand|YCBCR颜色模型中Cb波段。|
|YCbCr\_CrBand|YCBCR颜色模型中Cr波段。|

## 示例 {#section_lmw_qhn_qfb .section}

``` {#codeblock_hqr_1iy_h9v}
select ST_ColorInterp(raster_obj,0) from raster_table where id = 1;

__________________________________
RedBand
```

