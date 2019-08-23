# ST\_difference {#reference_jtm_syn_qfb .reference}

给定时间段的轨迹和给定的几何对象执行相差处理，返回相交处理后的轨迹对象。

## 语法 {#section_og1_4hn_qfb .section}

```
trajectory ST_difference(trajectory traj, tsrange range, geometry g);
trajectory ST_difference(trajectory traj, timestamp t1, timestamp t2, geometry g);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|
|t1|开始时间。|
|t2|结束时间。|
|range|时间段。|
|g|几何对象。|

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_difference(traj, '2010-1-1 13:00:00', '2010-1-1 14:00:00', 'LINSTRING(0 0, 5 5, 9 9)'::geometry) from  traj_table;
```

