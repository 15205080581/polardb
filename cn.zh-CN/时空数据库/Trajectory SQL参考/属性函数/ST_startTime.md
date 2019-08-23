# ST\_startTime {#reference_lfr_mhn_qfb .reference}

获得轨迹的起始时间。

## 语法 {#section_og1_4hn_qfb .section}

```
timestamp ST_startTime(trajectory traj) ;
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|需要获得开始时间的轨迹。|

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_startTime(traj) From traj_table;
```

