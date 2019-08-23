# ST\_intersection {#reference_qjy_ryn_qfb .reference}

给定时间段的轨迹和给定的几何对象执行相交处理，返回相交处理后的轨迹对象。

## 语法 {#section_og1_4hn_qfb .section}

``` {#codeblock_25k_lad_qjw}
trajectory[] ST_intersection(trajectory traj, tsrange range, geometry g);
trajectory[] ST_intersection(trajectory traj, timestamp t1, timestamp t2, geometry g);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|
|t1|开始时间。|
|t2|结束时间。|
|range|时间段。|
|g|几何对象。|

## 描述 {#section_b2r_1t8_uhw .section}

如果轨迹几何对象和几何对象有多个交点，则返回多个子轨迹。

## 示例 {#section_lmw_qhn_qfb .section}

``` {#codeblock_lce_1y1_jqk}
Select ST_intersection(traj, '2010-1-1 13:00:00', '2010-1-1 14:00:00', 'LINSTRING(0 0, 5 5, 9 9)'::geometry) from  traj_table;
```

