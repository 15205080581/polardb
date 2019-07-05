# ST\_mdistance {#reference_rpz_zb4_qfb .reference}

计算轨迹对象中所有相同的时间点的欧几里得距离。

## 语法 {#section_og1_4hn_qfb .section}

``` {#codeblock_efa_ewf_4dg}
float[] ST_mdistance(trajectory traj1, trajectory traj2);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj1|轨迹对象1。|
|traj2|轨迹对象2。|

## 描述 {#section_fdf_vtw_ca6 .section}

未经过标准化处理。

## 示例 {#section_lmw_qhn_qfb .section}

``` {#codeblock_bbl_rhs_xt0}
Select ST_mDistance((Select traj from traj_table where id=1), (Select traj from traj_table where id=2));
```

