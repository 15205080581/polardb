# ST\_distanceWithin {#reference_y2v_kyn_qfb .reference}

指定时间区间的轨迹段离给定几何对象在指定距离之内。

## 语法 {#section_og1_4hn_qfb .section}

```
boolean ST_distanceWithin(trajectory traj, tsrange range, geometry g, float8 d);
boolean ST_distanceWithin(trajectory traj, timestamp t1, timestamp t2, geometry g, float8 d);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|
|t1|开始时间。|
|t2|结束时间。|
|range|时间段。|
|g|几何对象。|
|d|距离。|

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_distanceWithin(traj, '2010-1-1 13:00:00', '2010-1-1 14:00:00', 'LINSTRING(0 0, 5 5, 9 9)'::geometry, 10) from  traj_table;
```

