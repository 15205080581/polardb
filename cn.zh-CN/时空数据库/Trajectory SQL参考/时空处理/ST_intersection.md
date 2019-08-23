# ST\_intersection {#reference_v1h_y14_qfb .reference}

定时间段的轨迹1和轨迹2执行对应时间点上的移动对象之间的空间Intersection处理。

## 语法 {#section_og1_4hn_qfb .section}

```
geometry ST_intersection(trajectory traj1, trajectory traj2, tsrange range);
geometry ST_intersection(trajectory traj1, trajectory traj2, timestamp t1, timestamp t2);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj1|轨迹对象1。|
|traj2|轨迹对象2。|
|t1|开始时间。|
|t2|结束时间。|
|range|时间段。|

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_intersection((Select traj from traj_table where id=1), (Select traj from traj_table where id=2), '2010-1-1 13:00:00', '2010-1-1 14:00:00');
```

