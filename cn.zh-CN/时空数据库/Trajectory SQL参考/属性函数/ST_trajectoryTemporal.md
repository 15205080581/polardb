# ST\_trajectoryTemporal {#reference_lfr_mhn_qfb .reference}

获得轨迹的时间线。

## 语法 {#section_og1_4hn_qfb .section}

``` {#codeblock_2jd_9ue_tb2}
text ST_trajectoryTemporal(trajectory traj);
text ST_trajTemporal(trajectory traj);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|需要获得时间线的轨迹。|

## 示例 {#section_lmw_qhn_qfb .section}

``` {#codeblock_o9m_7um_eno}
select ST_trajectoryTemporal(ST_MakeTrajectory('STPOINT'::leaftype, st_geomfromtext('LINESTRING (114 35, 115 36, 116 37)', 4326), '[2010-01-01 14:30, 2010-01-01 15:30)'::tsrange, null));
                              st_trajectorytemporal                             
--------------------------------------------------------------------------------
 {"timeline":["2010-01-01 14:30:00","2010-01-01 15:00:00","2010-01-01 15:30:00"]}
(1 row)
```

