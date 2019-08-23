# ST\_timeAtDistance {#reference_ofz_ksn_qfb .reference}

从起始点移动指定距离后所在的时间点。

## 语法 {#section_og1_4hn_qfb .section}

```
timestamp[] ST_timeAtDistance(trajectory traj, float8 d);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|
|d|距离。|

返回的是 timestamp的数组，有可能存在多个点到起始点的距离一致。

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_timeAtDistance(traj, 100) from traj_table;
```

