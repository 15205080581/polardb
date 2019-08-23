# ST\_timeAtCumulativeDistance {#reference_rvd_msn_qfb .reference}

从起点出发位移到指定长度时所处的时间点。

## 语法 {#section_og1_4hn_qfb .section}

```
timestamp ST_timeAtCumulativeDistance(trajectory traj, float d) ;
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|
|d|累计长度。|

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_timeAtCumulativeDistance(traj, 100.0) from traj_table;
```

