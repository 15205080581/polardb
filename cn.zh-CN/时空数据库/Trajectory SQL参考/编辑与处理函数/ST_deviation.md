# ST\_deviation {#reference_wny_rqp_3gb .reference}

计算处理后的轨迹与原始轨迹之间的偏差。

## 语法 {#section_og1_4hn_qfb .section}

```
trajectory ST_deviation(trajectory traj, trajectory after_oper_traj);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|原始轨迹对象。|
|after\_oper\_traj|处理后的轨迹对象（比如压缩后）。|

## 示例 {#section_lmw_qhn_qfb .section}

```
select st_deviation(traj, st_compress(traj,0.001)) from traj_test;
    st_deviation     
--------------------- 
0.00919177345596219
(1 row)
```

