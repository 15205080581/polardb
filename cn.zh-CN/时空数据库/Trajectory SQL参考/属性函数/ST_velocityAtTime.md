# ST\_velocityAtTime {#reference_t53_3sn_qfb .reference}

获取指定时间位置的速度属性。

## 语法 {#section_og1_4hn_qfb .section}

``` {#codeblock_hu9_od8_sko}
float8 ST_ VelocityAtTime (trajectory traj, timestamp t);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|
|t|指定的时间点。|

## 示例 {#section_lmw_qhn_qfb .section}

``` {#codeblock_1la_ir7_5da}
SeSelect ST_velocityAtTime(traj) From traj_table;
```

