# ST\_trajectorySpatial {#reference_lfr_mhn_qfb4 .reference}

获得轨迹的几何对象。

## 语法 {#section_og1_4hn_qfb .section}

``` {#codeblock_w5n_72i_o1d}
geometry ST_trajectorySpatial(trajectory traj);
geometry ST_trajSpatial(trajectory traj);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|需要获得几何对象的轨迹。|

## 示例 {#section_lmw_qhn_qfb .section}

``` {#codeblock_fwn_z2w_i6o}
Select AsText(ST_trajectorySpatial(traj)) FROM traj_table;
```

