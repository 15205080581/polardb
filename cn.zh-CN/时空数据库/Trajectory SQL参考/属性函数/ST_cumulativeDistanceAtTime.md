# ST\_cumulativeDistanceAtTime {#reference_p2p_lsn_qfb .reference}

从起点出发到指定时间点累计的位移长度。

## 语法 {#section_og1_4hn_qfb .section}

```
float8 ST_cumulativeDistanceAtTime(trajectory traj, timestamp t) ;
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|
|t|时间点。|

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_cumulativeDistanceAtTime(traj, '2011-11-1 04:30:00') from traj_table;
```

