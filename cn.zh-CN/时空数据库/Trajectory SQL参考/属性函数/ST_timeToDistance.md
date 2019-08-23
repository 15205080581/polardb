# ST\_timeToDistance {#reference_i5l_ksn_qfb .reference}

输出时间到欧氏距离的函数，以折线输出，横坐标为时间，纵坐标为距离。

## 语法 {#section_og1_4hn_qfb .section}

```
geometry ST_timeToDistance(trajectory traj);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|

## 示例 {#section_lmw_qhn_qfb .section}

```
Select ST_timeToDistance(traj) from traj_table;
```

