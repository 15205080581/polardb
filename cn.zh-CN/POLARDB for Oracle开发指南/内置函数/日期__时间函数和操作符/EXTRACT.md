# EXTRACT {#concept_221784 .concept}

函数EXTRACT用于从日期/时间字段中获取像年份或小时这样的子字段。函数EXTRACT返回值的类型是DOUBLE PRECISION。

## YEAR {#section_h4a_8j7_x66 .section}

表示年的字段。

``` {#codeblock_mkx_kue_p3y}
SELECT EXTRACT(YEAR FROM TIMESTAMP '2001-02-16 20:38:40') FROM DUAL;

 date_part
-----------
      2001
(1 row)		
```

## MONTH {#section_jxo_8og_abe .section}

表示一年中的月份（1-12）。

``` {#codeblock_w6z_y3y_7wg}
SELECT EXTRACT(MONTH FROM TIMESTAMP '2001-02-16 20:38:40') FROM DUAL;

 date_part
-----------
         2
(1 row)		
```

## DAY {#section_bsp_zbz_5rj .section}

表示一个月中的日期（1-31）。

``` {#codeblock_stf_ec9_xkp}
SELECT EXTRACT(DAY FROM TIMESTAMP '2001-02-16 20:38:40') FROM DUAL;

 date_part
-----------
        16
(1 row)		
```

## HOUR {#section_5cy_w2h_b2t .section}

表示小时字段（0-23）。

``` {#codeblock_cf4_zjd_9ii}
SELECT EXTRACT(HOUR FROM TIMESTAMP '2001-02-16 20:38:40') FROM DUAL;

 date_part
-----------
        20
(1 row)		
```

## MINUTE {#section_aft_dln_x4s .section}

表示分钟字段（0-59）。

``` {#codeblock_bmv_oso_txm}
SELECT EXTRACT(MINUTE FROM TIMESTAMP '2001-02-16 20:38:40') FROM DUAL;

 date_part
-----------
        38
(1 row)	
```

## SECOND {#section_989_f05_j2s .section}

表示秒字段，包含小数部分（0-59）。

``` {#codeblock_qki_pl5_rxu}
SELECT EXTRACT(SECOND FROM TIMESTAMP '2001-02-16 20:38:40') FROM DUAL;

 date_part
-----------
        40
(1 row)
```

