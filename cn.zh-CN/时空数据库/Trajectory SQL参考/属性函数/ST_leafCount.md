# ST\_leafCount {#reference_lfr_mhn_qfb .reference}

获得轨迹的叶子数量（轨迹点个数）。

## 语法 {#section_og1_4hn_qfb .section}

``` {#codeblock_ycf_yf3_0dd}
integer ST_leafCount(trajectory traj);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|需要获得类型的轨迹。|

## 示例 {#section_lmw_qhn_qfb .section}

``` {#codeblock_1ye_e3a_nm5}
select st_leafCount(traj) from traj where id = 2;
 st_leafcount 
--------------           
16
```

