# ST​\_nearestApproachPoint {#reference_jdl_hzn_qfb .reference}

指定时间段的轨迹中找到与给定几何对象最邻近点信息。

## 语法 {#section_og1_4hn_qfb .section}

```
geometry ST_nearestApproachPoint(trajectory traj, tsrange range, geometry g);
geometry ST_nearestApproachPoint(trajectory traj, timestamp t1, timestamp t2, geometry g);
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
Select ST​_nearestApproachPoint(traj, '2010-1-1 13:00:00', '2010-1-1 14:00:00', 'LINSTRING(0 0, 5 5, 9 9)'::geometry) from  traj_table;
```

