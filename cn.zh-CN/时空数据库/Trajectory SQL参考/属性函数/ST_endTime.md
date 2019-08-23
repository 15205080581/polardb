# ST\_endTime {#reference_lfr_mhn_qfb3 .reference}

获得轨迹的结束时间。

## 语法 {#section_og1_4hn_qfb .section}

```
timestamp ST_endTime(trajectory traj) ;
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|需要获得结束时间的轨迹。|

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_endTime(traj) From traj_table;
```

