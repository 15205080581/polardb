# ST\_equals {#reference_n3n_zzn_qfb .reference}

指定时间区间的轨迹段1和轨迹段2空间是否相等。

## 语法 {#section_og1_4hn_qfb .section}

```
boolean ST_equals(trajectory traj1, trajectory traj2, tsrange range);
boolean ST_equals(trajectory traj1, trajectory traj2, timestamp t1, timestamp t2);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|
|t1|开始时间。|
|t2|结束时间。|
|range|时间段。|

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_equals((Select traj from traj_table where id=1), (Select traj from traj_table where id=2), '2010-1-1 13:00:00', '2010-1-1 14:00:00');
```

