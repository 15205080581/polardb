# ST\_subTrajectory {#reference_cht_msn_qfb .reference}

根据时间段截取子段。

## 语法 {#section_og1_4hn_qfb .section}

```
trajectory ST_subTrajectory(trajectory traj, timestamp starttime, timestamp endtime）; 
trajectory ST_subTrajectory(trajectory traj, tsrange range);
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
Select ST_subTrajectory(traj, '2010-1-11 02:45:30', '2010-1-11 03:00:00') FROM traj_table;
```

