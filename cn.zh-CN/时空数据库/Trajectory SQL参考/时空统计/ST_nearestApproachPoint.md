# ST​\_nearestApproachPoint {#reference_m5l_jb4_qfb .reference}

指定时间段的轨迹1和轨迹2中找到最邻近点信息。

## 语法 {#section_og1_4hn_qfb .section}

``` {#codeblock_gaj_cua_bua}
geometry ST_nearestApproachPoint(trajectory traj1, trajectory traj2);
geometry ST_nearestApproachPoint(trajectory traj1, trajectory traj2,tsrange range);
geometry ST_nearestApproachPoint(trajectory traj1, trajectory traj2, timestamp t1, timestamp t2);
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

``` {#codeblock_r7g_pd7_1xx}
Select ST_nearestApproachPoint((Select traj from traj_table where id=1), (Select traj from traj_table where id=2), '2010-1-1 13:00:00', '2010-1-1 14:00:00');
```

