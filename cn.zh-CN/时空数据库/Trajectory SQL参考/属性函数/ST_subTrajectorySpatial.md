# ST\_subTrajectorySpatial {#reference_hzf_nsn_qfb .reference}

指定时间段的轨迹几何。

## 语法 {#section_og1_4hn_qfb .section}

```
geometry ST_subTrajectorySpatial(trajectory traj, timestamp starttime, timestamp endtime）;
geometry ST_subTrajectorySpatial(trajectory traj, tsrange range）;
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|
|starttime|开始时间。|
|endtime|结束时间。|
|range|时间段。|

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_subTrajectorySpatial(traj, '2010-1-11 02:45:30', '2010-1-11 03:00:00') FROM traj_table;
```

