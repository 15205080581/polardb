# ST\_duration {#reference_lfr_mhn_qfb9 .reference}

获得该轨迹的持续时间。

## 语法 {#section_og1_4hn_qfb .section}

``` {#codeblock_0s0_tys_djc}
interval ST_uration(trajectory traj);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹数据。|

## 示例 {#section_lmw_qhn_qfb .section}

``` {#codeblock_0hf_lhl_pgt}
select st_duration(traj) from traj where id = 2;
 st_duration 
-------------
 00:42:10
(1 row)
```

