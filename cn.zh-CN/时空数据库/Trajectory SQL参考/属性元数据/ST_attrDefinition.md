# ST\_attrDefinition {#reference_qmv_5qp_3gb .reference}

获得轨迹属性定义。

## 语法 {#section_og1_4hn_qfb .section}

```
t​ext ST_attrDefinition(trajectory traj);
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|需要获得属性定义轨迹。|

## 示例 {#section_lmw_qhn_qfb .section}

```
With traj AS (
  select '{"trajectory":{"version":1,"type":"STPOINT","leafcount":2,"start_time":"2010-01-01 11:30:00","end_time":"2010-01-01 12:30:00","spatial":"SRID=4326;LINESTRING(1 1,3 5)","timeline":["2010-01-01 11:30:00","2010-01-01 12:30:00"],"attributes":{"leafcount":2,"velocity":{"type":"integer","length":4,"nullable":true,"value":[1,null]},"speed":{"type":"float","length":8,"nullable":true,"value":[null,1.0]},"angel":{"type":"string","length":64,"nullable":true,"value":["test",null]}, "tngel2":{"type":"timestamp","length":8,"nullable":true,"value":["2010-01-01 12:30:00",null]},"bearing":{"type":"bool","length":1,"nullable":true,"value":[null,true]}}}}'::trajectory a)
Select st_attrDefinition(a) from traj;
                                                                                                                                      st_attrdefinition                                                                                                                                      
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 {"size":5,"velocity":{"type":"integer","length":4,"nullable":true},"speed":{"type":"float","length":8,"nullable":true},"angel":{"type":"string","length":64,"nullable":true},"tngel2":{"type":"timestamp","length":8,"nullable":true},"bearing":{"type":"bool","length":1,"nullable":true}}
(1 row)
```

