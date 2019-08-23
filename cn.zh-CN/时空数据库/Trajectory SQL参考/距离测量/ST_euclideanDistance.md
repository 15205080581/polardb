# ST\_euclideanDistance {#reference_f5z_xb4_qfb .reference}

计算两个轨迹对象之间的欧几里得距离。

## 语法 {#section_og1_4hn_qfb .section}

``` {#codeblock_5ng_w3k_ibl}
float ST_euclideanDistance(trajectory traj1, trajectory traj2);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj1|轨迹对象1。|
|traj2|轨迹对象2。|

## 描述 {#section_gzg_q5b_vtu .section}

距离已经进行了标准化处理。

## 示例 {#section_lmw_qhn_qfb .section}

``` {#codeblock_x4z_vm0_o2e}
Select ST_euclideanDistance((Select traj from traj_table where id=1), (Select traj from traj_table where id=2));
```

