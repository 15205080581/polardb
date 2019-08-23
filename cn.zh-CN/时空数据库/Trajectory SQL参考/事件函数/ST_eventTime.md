# ST\_eventTime {#reference_kcv_5wp_3gb .reference}

获得轨迹指定索引事件时间。

## 语法 {#section_og1_4hn_qfb .section}

```
timestamp ST_eventTime(trajectory traj, integer index) ;
```

## 参数 {#section_cxv_qhn_qfb .section}

|参数名称|描述|
|----|--|
|traj|轨迹对象。|
|index|事件索引序号。|

## 示例 {#section_lmw_qhn_qfb .section}

```
With traj AS (
  select '{"trajectory":{"version":1,"type":"STPOINT","leafcount":2,"start_time":"2010-01-01 11:30:00","end_time":"2010-01-01 12:30:00","spatial":"SRID=4326;LINESTRING(1 1,3 5)","timeline":["2010-01-01 11:30:00","2010-01-01 12:30:00"],"attributes":{"leafcount":2,"velocity":{"type":"integer","length":4,"nullable":true,"value":[1,null]},"speed":{"type":"float","length":8,"nullable":true,"value":[null,1.0]},"angel":{"type":"string","length":64,"nullable":true,"value":["test",null]}, "tngel2":{"type":"timestamp","length":8,"nullable":true,"value":["2010-01-01 12:30:00",null]},"bearing":{"type":"bool","length":1,"nullable":true,"value":[null,true]}},"events":[{"1":"Fri Jan 01 14:30:00 2010"}]}}'::trajectory a)
Select st_eventTime(a, 0 ) from traj;
    st_eventtime     
---------------------
 2010-01-01 14:30:00
(1 row)
```

