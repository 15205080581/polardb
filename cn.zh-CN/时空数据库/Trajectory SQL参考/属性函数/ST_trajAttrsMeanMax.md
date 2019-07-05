# ST\_trajAttrsMeanMax {#reference_995227 .reference}

根据MEAN-MAX算法，计算出每个时间段内的均值的最大值。

## 语法 {#section_uao_426_2h7 .section}

``` {#codeblock_vgi_4o2_0x0}
SETOF recrod ST_trajAttrsMeanMax(trajectory traj, cstring attr_field_name, out interval duration, out float8 max);
```

## 参数 {#section_a5y_f8e_4um .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|
|attr\_field\_name|指定的属性名称。|

## 描述 {#section_x1a_gle_zko .section}

Mean-Max 算法通过一个滑动窗口，分别计算出落入该窗口的属性值的平均值，再求出所有均值的最大值。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803581/156231348350858_zh-CN.png)

该函数仅对integer和float类型的属性值有效。属性值不能为NULL。

## 示例 {#section_csz_h5a_s1c .section}

``` {#codeblock_qdn_ifm_fwx}
With traj AS (
    Select ST_m akeTrajectory('STPO INT', 'LINESTRING(1 1, 6 6, 9 8, 10 12)'::geom etry,
    ARRAY['2010-01-01 11:30'::tim estam p, '2010-01-01 12:30', '2010-01-01 13:30', '2010-01-01 14:30'],'{"leafcount":4, "attributes":{"velocity": {"type": "float", "length":8,"nullable" : true,"value": [120.0, 130.0, 140.0, 120.0]}, "power": {"type": "float", "length": 4,"nullable" : true,"value": [120.0, 130.0, 140.0, 120.0]}}}') a)
Select st_trajAttrsMeanMax(a, 'velocity') from traj;
st_trajattrsm eanm ax
---------------------
("@ 1 hour",135)
("@ 2 hours",130)
("@ 3 hours",127.5)
(3 rows)

With traj AS (
    Select ST_m akeTrajectory('STPO INT', 'LINESTRING(1 1, 6 6, 9 8, 10 12)'::geom etry,
    ARRAY['2010-01-01 11:30'::tim estam p, '2010-01-01 12:30', '2010-01-01 13:30', '2010-01-01 14:30'], '{"leafcount":4, "attributes":{"velocity": {"type": "float", "length": 8,"nullable" : true,"value": [120.0, 130.0, 140.0, 120.0]}, "power": {"type": "float", "length": 4,"nullable" : true,"value": [120.0, 130.0, 140.0, 120.0]}}}') a)
Select (st_trajAttrsMeanMax(a, 'velocity')).* from traj;
 duration | m ax
----------+-------
 01:00:00 | 135
 02:00:00 | 130
 03:00:00 | 127.5
(3 rows)
```

