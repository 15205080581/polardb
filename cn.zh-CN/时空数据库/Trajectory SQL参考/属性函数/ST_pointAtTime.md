# ST\_pointAtTime {#reference_vhw_hsn_qfb .reference}

获取指定时间位置的几何对象。

## 语法 {#section_og1_4hn_qfb .section}

```
geometry ST_pointAtTime(trajectory traj, timestamp t);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|
|t|指定的时间点。|

返回点对象。

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_pointAtTime(traj, '2010-1-11 23:40:00') from traj_table;
```

