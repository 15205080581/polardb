# DBMS\_SQL {#concept_221989 .concept}

包DBMS\_SQL对EnterpriseDB的动态SQL查询功能提供用包DBMS\_SQL，可以在应用的运行时间构建查询和其它的命令（而不是在编写程序的时候完成这项工作）。EnterpriseDB Advance Server提供对动态SQL的特有支持；包DBMS\_SQL以一种与Oracle兼容的方式来使用动态SQL, 这样我们就无需修改程序了。

包DBMS\_SQL假定当前执行动态SQL的用户拥有相应的权限。

|Function/Procedure|Function or Procedure|Return Type|Description|
|------------------|---------------------|-----------|-----------|
|BIND\_VARIABLE\(c, name, value \[, out\_value\_size \]\)|Procedure|n/a|Bind a value to a variable.|
|BIND\_VARIABLE\_CHAR\(c, name, value \[, out\_value\_size \]\)|Procedure|n/a|Bind a CHAR value to a variable.|
|BIND\_VARIABLE\_RAW\(c, name, value \[, out\_value\_size \]\)|Procedure|n/a|Bind a RAW value to a variable.|
|CLOSE\_CURSOR\(c IN OUT\)|Procedure|n/a|Close a cursor.|
|COLUMN\_VALUE\(c, position, value OUT \[, column\_error OUT \[, actual\_length OUT \]\]\)|Procedure|n/a|Return a column value into a variable.|
|COLUMN\_VALUE\_CHAR\(c, position, value OUT \[, column\_error OUT \[, actual\_length OUT \]\]\)|Procedure|n/a|Return a CHAR column value into a variable.|
|COLUMN\_VALUE\_RAW\(c, position, value OUT \[, column\_error OUT \[, actual\_length OUT \]\]\)|Procedure|n/a|Return a RAW column value into a variable.|
|DEFINE\_COLUMN\(c, position, column \[, column\_size \]\)|Procedure|n/a|Define a column in the SELECT list.|
|DEFINE\_COLUMN\_CHAR\(c, position, column, column\_size\)|Procedure|n/a|Define a CHAR column in the SELECT list.|
|DEFINE\_COLUMN\_RAW\(c, position, column, column\_size\)|Procedure|n/a|Define a RAW column in the SELECT list.|
|DESCRIBE\_COLUMNS|Procedure|n/a|Defines columns to hold a cursor result set.|
|EXECUTE\(c\)|Function|INTEGER|Execute a cursor.|
|EXECUTE\_AND\_FETCH\(c \[, exact \]\)|Function|INTEGER|Execute a cursor and fetch a single row.|
|FETCH\_ROWS\(c\)|Function|INTEGER|Fetch rows from the cursor.|
|IS\_OPEN\(c\)|Function|BOOLEAN|Check if a cursor is open.|
|LAST\_ROW\_COUNT|Function|INTEGER|Return cumulative number of rows fetched.|
|OPEN\_CURSOR|Function|INTEGER|Open a cursor.|
|PARSE\(c, statement, language\_flag\)|Procedure|n/a|Parse a statement.|

与Oracle版本的DBMS\_SQL执行相比，POLARDB for Oracle的DBMS\_SQL执行是部分执行。POLARDB for Oracle仅支持上述表中列出的函数和存储过程。

下面的表中列出了在包DBM\_SQL允许使用的公有变量。

|Public Variables|Data Type|Value|Description|
|----------------|---------|-----|-----------|
|native|INTEGER|1|Provided for compatibility with Oracle syntax. See DBMS\_SQL.PARSE for more information.|
|V6|INTEGER|2|Provided for compatibility with Oracle syntax. See DBMS\_SQL.PARSE for more information.|
|V7|INTEGER|3|Provided for compatibility with Oracle syntax. See DBMS\_SQL.PARSE for more information|

## BIND\_VARIABLE {#section_ksv_ixb_lm7 .section}

存储过程BIND\_VARIABLE用于将一个值和在SQL命令中的IN或IN OUT绑定变量相关联。

``` {#codeblock_p9c_nks_rtk}
BIND_VARIABLE(c INTEGER, name VARCHAR2,
  value { BLOB | CLOB | DATE | FLOAT | INTEGER | NUMBER |
          TIMESTAMP | VARCHAR2 }
  [, out_value_size INTEGER ])
```

**参数**

|参数名称|描述|
|----|--|
|c|与带有绑定变量SQL命令相对应游标的ID。|
|name|SQL命令中绑定变量的名称。|
|value|被分配的值。|
|out\_value\_size|如果name是一个IN OUT模式的变量，那么定义输出值的最大长度。如果没有指定这个参数，那么将当前value的长度默认为最大值长度。|

**示例**

下面的匿名代码块使用绑定变量向表emp中插入一条记录。

``` {#codeblock_ccc_prn_tpd}
DECLARE
    curid           INTEGER;
    v_sql           VARCHAR2(150) := 'INSERT INTO emp VALUES ' ||
                        '(:p_empno, :p_ename, :p_job, :p_mgr, ' ||
                        ':p_hiredate, :p_sal, :p_comm, :p_deptno)';
    v_empno         emp.empno%TYPE;
    v_ename         emp.ename%TYPE;
    v_job           emp.job%TYPE;
    v_mgr           emp.mgr%TYPE;
    v_hiredate      emp.hiredate%TYPE;
    v_sal           emp.sal%TYPE;
    v_comm          emp.comm%TYPE;
    v_deptno        emp.deptno%TYPE;
    v_status        INTEGER;
BEGIN
    curid := DBMS_SQL.OPEN_CURSOR;
    DBMS_SQL.PARSE(curid,v_sql,DBMS_SQL.native);
    v_empno    := 9001;
    v_ename    := 'JONES';
    v_job      := 'SALESMAN';
    v_mgr      := 7369;
    v_hiredate := TO_DATE('13-DEC-07','DD-MON-YY');
    v_sal      := 8500.00;
    v_comm     := 1500.00;
    v_deptno   := 40;
    DBMS_SQL.BIND_VARIABLE(curid,':p_empno',v_empno);
    DBMS_SQL.BIND_VARIABLE(curid,':p_ename',v_ename);
    DBMS_SQL.BIND_VARIABLE(curid,':p_job',v_job);
    DBMS_SQL.BIND_VARIABLE(curid,':p_mgr',v_mgr);
    DBMS_SQL.BIND_VARIABLE(curid,':p_hiredate',v_hiredate);
    DBMS_SQL.BIND_VARIABLE(curid,':p_sal',v_sal);
    DBMS_SQL.BIND_VARIABLE(curid,':p_comm',v_comm);
    DBMS_SQL.BIND_VARIABLE(curid,':p_deptno',v_deptno);
    v_status := DBMS_SQL.EXECUTE(curid);
    DBMS_OUTPUT.PUT_LINE('Number of rows processed: ' || v_status);
    DBMS_SQL.CLOSE_CURSOR(curid);
END;

Number of rows processed: 1
```

## BIND\_VARIABLE\_CHAR {#section_f37_cwh_cpc .section}

存储过程BIND\_VARIABLE\_CHAR将一个CHAR类型值和SQL命令中的IN或IN OUT绑定变量相关联。

``` {#codeblock_ikz_exk_7ba}
BIND_VARIABLE_CHAR(c INTEGER, name VARCHAR2, value CHAR
  [, out_value_size INTEGER ])
```

**参数**

|参数名称|描述|
|----|--|
|c|与带有绑定变量的SQL命令相对应的游标ID。|
|name|SQL命令中绑定变量的名称。|
|value|被分配的类型为RAW的值。|
|out\_value\_size|如果name是一个IN OUT模式的变量，那么定义输出值的最大长度。如果没有指定这个参数，那么将当前值的长度默认为最大值长度。|

## BIND VARIABLE RAW {#section_oj4_sy1_1wi .section}

存储过程BIND\_VARIABLE\_RAW用于将一个类型为RAW的值和SQL命令中的IN或IN OUT绑定变量相关联。

``` {#codeblock_fgc_ey4_o5k}
BIND_VARIABLE_RAW(c INTEGER, name VARCHAR2, value RAW
  [, out_value_size INTEGER ])
```

**参数**

|参数名称|描述|
|----|--|
|c|与带有绑定变量的SQL命令相对应的游标ID。|
|name|SQL命令中绑定变量的名称。|
|value|被分配的类型为RAW的值。|
|out\_value\_size|如果name是一个IN OUT模式的变量，那么定义输出值的最大长度。如果没有指定这个参数，那么将当前值的长度默认为最大值长度。|

## CLOSE\_CURSOR {#section_jd6_jr4_nfn .section}

存储过程CLOSE\_CURSOR关闭一个已打开的游标。当关闭游标后，释放分配给游标的资源，并且 不能再使用这个游标。

``` {#codeblock_1sd_egg_t1p}
CLOSE_CURSOR(c IN OUT INTEGER)
			
```

**参数**

|参数名称|描述|
|----|--|
|c|要关闭游标的ID。|

**示例**

在下面的示例中，关闭了一个先前已打开的游标：

``` {#codeblock_lko_yui_ma1}
DECLARE
    curid           INTEGER;
BEGIN
    curid := DBMS_SQL.OPEN_CURSOR;
            .
            .
            .
    DBMS_SQL.CLOSE_CURSOR(curid);
END;
```

## COLUMN\_VALUE {#section_189_vku_bkm .section}

存储过程COLUMN\_VALUE定义了一个变量，用于从游标中接收值。

``` {#codeblock_70q_g5s_mdx}
COLUMN_VALUE(c INTEGER, position INTEGER, value OUT { BLOB |
  CLOB | DATE | FLOAT | INTEGER | NUMBER | TIMESTAMP | VARCHAR2 }
  [, column_error OUT NUMBER [, actual_length OUT INTEGER ]])
```

**参数**

|参数名称|描述|
|----|--|
|c|一个游标的ID，用于将数据返回给被定义变量。|
|position|在游标中返回数据的位置。在游标中的第一个位置值是1。|
|value|通过前面的fetch操作在游标中接收返回数据的变量。|
|column\_error|如果发生异常错误，这个参数表示与列相关的错误代码。|
|actual\_length|在进行截断操作前，数据的实际长度。|

**示例**

下面的代码显示一个匿名代码块的一部分。这部分代码的功能是通过存储过程COLUMN\_VALUE，从游标中接收数据。

``` {#codeblock_lin_v20_23m}
DECLARE
    curid           INTEGER;
    v_empno         NUMBER(4);
    v_ename         VARCHAR2(10);
    v_hiredate      DATE;
    v_sal           NUMBER(7,2);
    v_comm          NUMBER(7,2);
    v_sql           VARCHAR2(50) := 'SELECT empno, ename, hiredate, sal, ' ||
                                    'comm FROM emp';
    v_status        INTEGER;
BEGIN
            .
            .
            .
    LOOP
        v_status := DBMS_SQL.FETCH_ROWS(curid);
        EXIT WHEN v_status = 0;
        DBMS_SQL.COLUMN_VALUE(curid,1,v_empno);
        DBMS_SQL.COLUMN_VALUE(curid,2,v_ename);
        DBMS_SQL.COLUMN_VALUE(curid,3,v_hiredate);
        DBMS_SQL.COLUMN_VALUE(curid,4,v_sal);
        DBMS_SQL.COLUMN_VALUE(curid,4,v_sal);
        DBMS_SQL.COLUMN_VALUE(curid,5,v_comm);
        DBMS_OUTPUT.PUT_LINE(v_empno || '   ' || RPAD(v_ename,10) || '  ' ||
            TO_CHAR(v_hiredate,'yyyy-mm-dd') || ' ' ||
            TO_CHAR(v_sal,'9,999.99') || ' ' ||
            TO_CHAR(NVL(v_comm,0),'9,999.99'));
    END LOOP;
    DBMS_SQL.CLOSE_CURSOR(curid);
END;
```

## COLUMN\_VALUE\_CHAR {#section_zh0_o6n_6zd .section}

存储过程COLUMN\_VALUE\_CHAR定义一个变量，用于从游标中接收一个CHAR类型的值。

``` {#codeblock_sul_v6u_7m1}
COLUMN_VALUE_CHAR(c INTEGER, position INTEGER, value OUT CHAR
  [, column_error OUT NUMBER [, actual_length OUT INTEGER ]])
```

**参数**

|参数名称|描述|
|----|--|
|c|游标的ID，用于向被定义的变量返回数据。|
|position|返回数据在游标内部的位置。在游标中的第一个位置是1。|
|value|类型为CHAR的变量，通过前面已经进行fetch操作，从游标中接收数据。|
|column\_error|如果有任何错误发生，这个参数表示与列相关的错误代码。|
|actual\_length|在任何截断的操作前，数据的实际长度。|

## COLUMN VALUE RAW {#section_pxt_57y_k15 .section}

存储过程COLUMN\_VALUE定义一个变量，用于从游标中接收一个RAW型的值。

``` {#codeblock_3t2_8kx_6rx}
COLUMN_VALUE_RAW(c INTEGER, position INTEGER, value OUT RAW
  [, column_error OUT NUMBER [, actual_length OUT INTEGER ]])
```

**参数**

|参数名称|描述|
|----|--|
|c|游标的ID，用于向被定义变量返回数据。|
|position|返回数据在游标中位置。在游标中的第一个值是1。|
|value|类型为RAW的变量，通过前面已经进行fetch操作，从游标中接收数据。|
|column\_error|如果有任何错误发生，这个参数表示与列相关的错误代码。|
|actual\_length|在任何截断的操作前，数据的实际长度。|

## DEFINE\_COLUMN {#section_z0x_dp3_uxd .section}

存储过程DEFINE\_COLUMN在SELECT列表中定义了一个列或者表达式，这个列或者表达式将在游标中返回和取出。

``` {#codeblock_sma_mf8_prb}
DEFINE_COLUMN(c INTEGER, position INTEGER, column { BLOB |
  CLOB | DATE | FLOAT | INTEGER | NUMBER | TIMESTAMP | VARCHAR2 }
  [, column_size INTEGER ])
```

**参数**

|参数名称|描述|
|----|--|
|c|与SELECT命令相关联的游标ID。|
|position|被定义的列或者表达式在SELECT列表中的位置。|
|column|在SELECT列表中位置为position的列或者表达式数据类型相等的变量。|
|column\_size|返回数据的最大长度。如果列的数据类型是VARCHAR2, 那么必须指定column\_size。长度超过column\_size的返回数据将被截断为长度是column\_size的字符串。|

**示例**

下面显示了如何使用存储过程DEFINE\_COLUMN定义表emp的列empno, ename, hiredate, sal, 和comm

``` {#codeblock_8gv_qav_vha}
DECLARE
    curid           INTEGER;
    v_empno         NUMBER(4);
    v_ename         VARCHAR2(10);
    v_hiredate      DATE;
    v_sal           NUMBER(7,2);
    v_comm          NUMBER(7,2);
    v_sql           VARCHAR2(50) := 'SELECT empno, ename, hiredate, sal, ' ||
                                    'comm FROM emp';
    v_status        INTEGER;
BEGIN
    curid := DBMS_SQL.OPEN_CURSOR;
    DBMS_SQL.PARSE(curid,v_sql,DBMS_SQL.native);
    DBMS_SQL.DEFINE_COLUMN(curid,1,v_empno);
    DBMS_SQL.DEFINE_COLUMN(curid,2,v_ename,10);
    DBMS_SQL.DEFINE_COLUMN(curid,3,v_hiredate);
    DBMS_SQL.DEFINE_COLUMN(curid,4,v_sal);
    DBMS_SQL.DEFINE_COLUMN(curid,5,v_comm);
            .
            .
            .
END;
```

下面显示了针对上个示例的另外一种实现方法，产生的结果完全一样。需要注意的是与数据类型的 长度无关-列empno,sal,和comm返回的数据长度分别等于NUMBER\(4\)和NUMBER\(7,2\)，尽管v\_num是被 定义为NUMBER\(1\)\(假定在存储过程COLUMN\_VALUE中的声明是最大长度）.列ename将返回的数据长度 可达到调用存储过程DEFINE\_COLUMN中定义的长度参数，而不是对于v\_varchar声明中类型VARCHAR2\(1\).返回数据的实际长度是由存储过程COLUMN\_VALUE来规定的。

``` {#codeblock_07k_c41_a7x}
DECLARE
    curid           INTEGER;
    v_num           NUMBER(1);
    v_varchar       VARCHAR2(1);
    v_date          DATE;
    v_sql           VARCHAR2(50) := 'SELECT empno, ename, hiredate, sal, ' ||
                                    'comm FROM emp';
    v_status        INTEGER;
BEGIN
    curid := DBMS_SQL.OPEN_CURSOR;
    DBMS_SQL.PARSE(curid,v_sql,DBMS_SQL.native);
    DBMS_SQL.DEFINE_COLUMN(curid,1,v_num);
    DBMS_SQL.DEFINE_COLUMN(curid,2,v_varchar,10);
    DBMS_SQL.DEFINE_COLUMN(curid,3,v_date);
    DBMS_SQL.DEFINE_COLUMN(curid,4,v_num);
    DBMS_SQL.DEFINE_COLUMN(curid,5,v_num);
            .
            .
            .
END;
```

## DEFINE\_COLUMN\_CHAR {#section_8mw_e8j_4ut .section}

存储过程DEFINE\_COLUMN\_CHAR在SELECT列表中定义了一个CHAR类型的列或表达式，我们在游标中返回并获取这个CHAR类型的列或表达式。

``` {#codeblock_8vs_owo_rlc}
DEFINE_COLUMN_CHAR(c INTEGER, position INTEGER, column CHAR, column_size INTEGER)
```

**参数**

|参数名称|描述|
|----|--|
|c|与SELECT命令相关的游标ID。|
|position|被定义的列或者表达式在SELECT列表中的位置。|
|column|一个CHAR类型变量。|
|column\_size|返回数据的最大长度，长度超过column\_size的返会数据将被截断为长度是column\_size的字符串。|

## DEFINE COLUMN RAW {#section_n6r_b3v_37x .section}

存储过程DEFINE\_COLUMN\_RAW在SELECT列表中定义了一个RAW类型的列或表达式，我们在游标中返回并获取这个RAW类型的列或表达式。

``` {#codeblock_hir_ia9_rpm}
DEFINE_COLUMN_RAW(c INTEGER, position INTEGER, column RAW,
  column_size INTEGER)
```

**参数**

|参数名称|描述|
|----|--|
|c|与SELECT命令相关的游标ID。|
|position|被定义的列或者表达式在SELECT列表中的位置。|
|column|一个RAW类型变量。|
|column\_size|返回数据的最大长度，当返回数据的长度超过column\_size时，将长度截断到column\_size。|

## DESCRIBE COLUMNS {#section_cnl_9tw_x24 .section}

DESCRIBE\_COLUMNS 存储过程用于描述游标返回的列。

``` {#codeblock_veg_po0_5yb}
DESCRIBE_COLUMNS(c INTEGER, col_cnt OUT INTEGER, desc_t OUT
  DESC_TAB);
```

**参数**

|参数名称|描述|
|----|--|
|c|游标的ID 。|
|col\_cnt|游标结果集中列的数量。|
|desc\_tab|包含游标所返回的每列的描述的表。描述为DESC\_REC 类型，包含值见下表。|

|Column Name|Type|
|-----------|----|
|col\_type|INTEGER|
|col\_max\_len|INTEGER|
|col\_name|VARCHAR2\(128\)|
|col\_name\_len|INTEGER|
|col\_schema\_name|VARCHAR2\(128\)|
|col\_schema\_name\_len|INTEGER|
|col\_precision|INTEGER|
|col\_scale|INTEGER|
|col\_charsetid|INTEGER|
|col\_charsetform|INTEGER|
|col\_null\_ok|BOOLEAN|

## EXECUTE {#section_vlx_rk9_h4s .section}

函数EXECUTE用于执行一个已解析SQL语句或SPL代码块。

``` {#codeblock_uzh_6mc_dhu}
status INTEGER EXECUTE(c INTEGER)
			
```

**参数**

|参数名称|描述|
|----|--|
|c|要执行的SQL语句或SPL代码块的游标ID，其中SQL命令已解析。|
|status|如果SQL命令是DELETE,INSERT或UPDATE,那么这个参数代表已处理的记录数。如果是其它命令，那么这个参数没有意义。|

**示例**

下面的匿名代码块向表dept中插入了一条记录。

``` {#codeblock_2xx_51s_ga3}
DECLARE
    curid           INTEGER;
    v_sql           VARCHAR2(50);
    v_status        INTEGER;
BEGIN
    curid := DBMS_SQL.OPEN_CURSOR;
    v_sql := 'INSERT INTO dept VALUES (50, ''HR'', ''LOS ANGELES'')';
    DBMS_SQL.PARSE(curid, v_sql, DBMS_SQL.native);
    v_status := DBMS_SQL.EXECUTE(curid);
    DBMS_OUTPUT.PUT_LINE('Number of rows processed: ' || v_status);
    DBMS_SQL.CLOSE_CURSOR(curid);
END;
```

## EXECUTE\_AND\_FETCH {#section_12w_858_mdc .section}

函数EXECUTE\_AND\_FETCH用于执行一条已解析的SELECT命令，并且取回一条记录。

``` {#codeblock_5fm_hnp_mmh}
status INTEGER EXECUTE_AND_FETCH(c INTEGER
  [, exact BOOLEAN ])
```

**参数**

|参数名称|描述|
|----|--|
|c|与要执行SELECT命令对应的游标ID。|
|exact|如果把这个参数设置为”true”,那么当结果集中的记录数不等于1的时候，就会产生一个异常。如果设置为”false”，则不会产生异常。这个参数缺省值是”false”。如果这个参数设置为”true”并且在结果集中没有记录，那么会产生一个NO\_DATE\_FOUND的异常。而在exact参数为”true”，并且在结果集中有多条记录的情况下，就会产生TOO\_MANY\_ROWS的异常。|
|status|如果成功取回一条记录，那么这个参数返回1。如果没有取回记录，那么这个参数返回为0。而如果产生异常的话，则这个参数不返回值。|

**示例**

下面这个存储过程使用函数EXECUTE\_AND\_FETCH 根据雇员的名称来取出一条雇员记录。如果没有找到相应的雇员记录，或者找到多个具有相同的名字的雇员，那么都会产生异常。

``` {#codeblock_2aw_oo2_w2j}
CREATE OR REPLACE PROCEDURE select_by_name(
    p_ename         emp.ename%TYPE
)
IS
    curid           INTEGER;
    v_empno         emp.empno%TYPE;
    v_hiredate      emp.hiredate%TYPE;
    v_sal           emp.sal%TYPE;
    v_comm          emp.comm%TYPE;
    v_dname         dept.dname%TYPE;
    v_disp_date     VARCHAR2(10);
    v_sql           VARCHAR2(120) := 'SELECT empno, hiredate, sal, ' ||
                                     'NVL(comm, 0), dname ' ||
                                     'FROM emp e, dept d ' ||
                                     'WHERE ename = :p_ename ' ||
                                     'AND e.deptno = d.deptno';
    v_status        INTEGER;
BEGIN
    curid := DBMS_SQL.OPEN_CURSOR;
    DBMS_SQL.PARSE(curid,v_sql,DBMS_SQL.native);
    DBMS_SQL.BIND_VARIABLE(curid,':p_ename',UPPER(p_ename));
    DBMS_SQL.DEFINE_COLUMN(curid,1,v_empno);
    DBMS_SQL.DEFINE_COLUMN(curid,2,v_hiredate);
    DBMS_SQL.DEFINE_COLUMN(curid,3,v_sal);
    DBMS_SQL.DEFINE_COLUMN(curid,4,v_comm);
    DBMS_SQL.DEFINE_COLUMN(curid,5,v_dname,14);
    v_status := DBMS_SQL.EXECUTE_AND_FETCH(curid,TRUE);
    DBMS_SQL.COLUMN_VALUE(curid,1,v_empno);
    DBMS_SQL.COLUMN_VALUE(curid,2,v_hiredate);
    DBMS_SQL.COLUMN_VALUE(curid,3,v_sal);
    DBMS_SQL.COLUMN_VALUE(curid,4,v_comm);
    DBMS_SQL.COLUMN_VALUE(curid,5,v_dname);
    v_disp_date := TO_CHAR(v_hiredate, 'MM/DD/YYYY');
    DBMS_OUTPUT.PUT_LINE('Number    : ' || v_empno);
    DBMS_OUTPUT.PUT_LINE('Name      : ' || UPPER(p_ename));
    DBMS_OUTPUT.PUT_LINE('Hire Date : ' || v_disp_date);
    DBMS_OUTPUT.PUT_LINE('Salary    : ' || v_sal);
    DBMS_OUTPUT.PUT_LINE('Commission: ' || v_comm);
    DBMS_OUTPUT.PUT_LINE('Department: ' || v_dname);
    DBMS_SQL.CLOSE_CURSOR(curid);
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Employee ' || p_ename || ' not found');
        DBMS_SQL.CLOSE_CURSOR(curid);
    WHEN TOO_MANY_ROWS THEN
        DBMS_OUTPUT.PUT_LINE('Too many employees named, ' ||
            p_ename || ', found');
        DBMS_SQL.CLOSE_CURSOR(curid);
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('The following is SQLERRM:');
        DBMS_OUTPUT.PUT_LINE(SQLERRM);
        DBMS_OUTPUT.PUT_LINE('The following is SQLCODE:');
        DBMS_OUTPUT.PUT_LINE(SQLCODE);
        DBMS_SQL.CLOSE_CURSOR(curid);
END;

EXEC select_by_name('MARTIN')

Number    : 7654
Name      : MARTIN
Hire Date : 09/28/1981
Salary    : 1250
Commission: 1400
Department: SALES
```

## FETCH\_ROWS {#section_31p_4si_hg2 .section}

函数FETCH\_ROWS从一个游标中获取一条记录。

``` {#codeblock_3ft_oxh_cvm}
status INTEGER FETCH_ROWS(c INTEGER)
			
```

**参数**

|参数名称|描述|
|----|--|
|c|用于获取记录的游标ID。|
|status|如果成功获取一条记录，这个参数返回1，如果没有取回记录，那么返回0。|

**示例**

在下面的示例中，我们从表emp中取出记录，并且显示结果。

``` {#codeblock_z5q_hbg_7h4}
DECLARE
    curid           INTEGER;
    v_empno         NUMBER(4);
    v_ename         VARCHAR2(10);
    v_hiredate      DATE;
    v_sal           NUMBER(7,2);
    v_comm          NUMBER(7,2);
    v_sql           VARCHAR2(50) := 'SELECT empno, ename, hiredate, sal, ' ||
                                    'comm FROM emp';
    v_status        INTEGER;
BEGIN
    curid := DBMS_SQL.OPEN_CURSOR;
    DBMS_SQL.PARSE(curid,v_sql,DBMS_SQL.native);
    DBMS_SQL.DEFINE_COLUMN(curid,1,v_empno);
    DBMS_SQL.DEFINE_COLUMN(curid,2,v_ename,10);
    DBMS_SQL.DEFINE_COLUMN(curid,3,v_hiredate);
    DBMS_SQL.DEFINE_COLUMN(curid,4,v_sal);
    DBMS_SQL.DEFINE_COLUMN(curid,5,v_comm);

    v_status := DBMS_SQL.EXECUTE(curid);
    DBMS_OUTPUT.PUT_LINE('EMPNO  ENAME       HIREDATE    SAL       COMM');
    DBMS_OUTPUT.PUT_LINE('-----  ----------  ----------  --------  ' ||
        '--------');
    LOOP
        v_status := DBMS_SQL.FETCH_ROWS(curid);
        EXIT WHEN v_status = 0;
        DBMS_SQL.COLUMN_VALUE(curid,1,v_empno);
        DBMS_SQL.COLUMN_VALUE(curid,2,v_ename);
        DBMS_SQL.COLUMN_VALUE(curid,3,v_hiredate);
        DBMS_SQL.COLUMN_VALUE(curid,4,v_sal);
        DBMS_SQL.COLUMN_VALUE(curid,4,v_sal);
        DBMS_SQL.COLUMN_VALUE(curid,5,v_comm);
        DBMS_OUTPUT.PUT_LINE(v_empno || '   ' || RPAD(v_ename,10) || '  ' ||
            TO_CHAR(v_hiredate,'yyyy-mm-dd') || ' ' ||
            TO_CHAR(v_sal,'9,999.99') || ' ' ||
            TO_CHAR(NVL(v_comm,0),'9,999.99'));
    END LOOP;
    DBMS_SQL.CLOSE_CURSOR(curid);
END;

EMPNO  ENAME       HIREDATE    SAL       COMM
-----  ----------  ----------  --------  --------
7369   SMITH       1980-12-17    800.00       .00
7499   ALLEN       1981-02-20  1,600.00    300.00
7521   WARD        1981-02-22  1,250.00    500.00
7566   JONES       1981-04-02  2,975.00       .00
7654   MARTIN      1981-09-28  1,250.00  1,400.00
7698   BLAKE       1981-05-01  2,850.00       .00
7782   CLARK       1981-06-09  2,450.00       .00
7788   SCOTT       1987-04-19  3,000.00       .00
7839   KING        1981-11-17  5,000.00       .00
7844   TURNER      1981-09-08  1,500.00       .00
7876   ADAMS       1987-05-23  1,100.00       .00
7900   JAMES       1981-12-03    950.00       .00
7902   FORD        1981-12-03  3,000.00       .00
7934   MILLER      1982-01-23  1,300.00       .00
```

## IS\_OPEN {#section_ned_9xr_wvb .section}

函数IS\_OPEN用于测试是否已打开一个游标。

``` {#codeblock_rcg_99u_vy4}
status BOOLEAN IS_OPEN(c INTEGER)
			
```

**参数**

|参数名称|描述|
|----|--|
|c|要测试游标的ID。|
|status|如果游标是打开状态，这个参数设为TRUE， 如果游标没有打开，那么这个值设为FALSE。|

## LAST ROW COUNT {#section_32h_e6m_y8p .section}

函数LAST\_ROW\_COUNT返回当前已取回记录的总数。

``` {#codeblock_o9j_58h_vhd}
rowcnt INTEGER LAST_ROW_COUNT
			
```

**参数**

|参数名称|描述|
|----|--|
|rowcnt|已取回记录的总数。|

**示例**

在下面的示例中，我们使用函数LAST\_ROW\_COUNT显示了查询中已取回记录的总数。

``` {#codeblock_q18_f0p_gv4}
DECLARE
    curid           INTEGER;
    v_empno         NUMBER(4);
    v_ename         VARCHAR2(10);
    v_hiredate      DATE;
    v_sal           NUMBER(7,2);
    v_comm          NUMBER(7,2);
    v_sql           VARCHAR2(50) := 'SELECT empno, ename, hiredate, sal, ' ||
                                    'comm FROM emp';
    v_status        INTEGER;
BEGIN
    curid := DBMS_SQL.OPEN_CURSOR;
    DBMS_SQL.PARSE(curid,v_sql,DBMS_SQL.native);
    DBMS_SQL.DEFINE_COLUMN(curid,1,v_empno);
    DBMS_SQL.DEFINE_COLUMN(curid,2,v_ename,10);
    DBMS_SQL.DEFINE_COLUMN(curid,3,v_hiredate);
    DBMS_SQL.DEFINE_COLUMN(curid,4,v_sal);
    DBMS_SQL.DEFINE_COLUMN(curid,5,v_comm);

    v_status := DBMS_SQL.EXECUTE(curid);
    DBMS_OUTPUT.PUT_LINE('EMPNO  ENAME       HIREDATE    SAL       COMM');
    DBMS_OUTPUT.PUT_LINE('-----  ----------  ----------  --------  ' ||
        '--------');
    LOOP
        v_status := DBMS_SQL.FETCH_ROWS(curid);
        EXIT WHEN v_status = 0;
        DBMS_SQL.COLUMN_VALUE(curid,1,v_empno);
        DBMS_SQL.COLUMN_VALUE(curid,2,v_ename);
        DBMS_SQL.COLUMN_VALUE(curid,3,v_hiredate);
        DBMS_SQL.COLUMN_VALUE(curid,4,v_sal);
        DBMS_SQL.COLUMN_VALUE(curid,4,v_sal);
        DBMS_SQL.COLUMN_VALUE(curid,5,v_comm);
        DBMS_OUTPUT.PUT_LINE(v_empno || '   ' || RPAD(v_ename,10) || '  ' ||
            TO_CHAR(v_hiredate,'yyyy-mm-dd') || ' ' ||
            TO_CHAR(v_sal,'9,999.99') || ' ' ||
            TO_CHAR(NVL(v_comm,0),'9,999.99'));
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Number of rows: ' || DBMS_SQL.LAST_ROW_COUNT);
    DBMS_SQL.CLOSE_CURSOR(curid);
END;

EMPNO  ENAME       HIREDATE    SAL       COMM
-----  ----------  ----------  --------  --------
7369   SMITH       1980-12-17    800.00       .00
7499   ALLEN       1981-02-20  1,600.00    300.00
7521   WARD        1981-02-22  1,250.00    500.00
7566   JONES       1981-04-02  2,975.00       .00
7654   MARTIN      1981-09-28  1,250.00  1,400.00
7698   BLAKE       1981-05-01  2,850.00       .00
7782   CLARK       1981-06-09  2,450.00       .00
7788   SCOTT       1987-04-19  3,000.00       .00
7839   KING        1981-11-17  5,000.00       .00
7844   TURNER      1981-09-08  1,500.00       .00
7876   ADAMS       1987-05-23  1,100.00       .00
7900   JAMES       1981-12-03    950.00       .00
7902   FORD        1981-12-03  3,000.00       .00
7934   MILLER      1982-01-23  1,300.00       .00
Number of rows: 14
```

## OPEN\_CURSOR {#section_zne_l99_z2y .section}

函数OPEN\_CURSOR用于创建一个新的游标。我们必须使用一个游标来解析和执行动态SQL语句。当打开游标后，可以以相同或不同的SQL语句来重复使用这个游标。我们不需要通过关闭然后重新打开的方式实现对游标进行重用。

``` {#codeblock_50z_mi6_f3t}
c INTEGER OPEN_CURSOR
			
```

**参数**

|参数名称|描述|
|----|--|
|c|与新创建的游标相关联的游标ID。|

**示例**

在下面的示例中创建了一个新的游标：

``` {#codeblock_rrj_rfu_dgw}
DECLARE
    curid           INTEGER;
BEGIN
    curid := DBMS_SQL.OPEN_CURSOR;
            .
            .
            .
END;
```

## PARSE {#section_tbb_m3n_asz .section}

存储过程PARSE用于解析一条SQL命令或SPL代码块。如果SQL语句是一条DDL命令，那么将立即执行这条命令，而不要求运行函数EXECUTE。

``` {#codeblock_vcq_i8g_abh}
PARSE(c INTEGER, statement VARCHAR2, language_flag INTEGER)
			
```

**参数**

|参数名称|描述|
|----|--|
|c|一个已打开游标的ID。|
|statement|已解析的SQL命令或SPL代码块。SQL命令不能以分号结束，而一个SPL代码块则要求以分号结束。|
|language\_flag|这个参数是为了与Oracle语法兼容而提供的。使用DBMS\_SQL.V6, DBMS\_SQL.V7 或DBMS\_SQL.native. 实际上我们可以忽略这个标志，所有的语法都假定是以EnterpriseDB Advanced Server的形式存在的。|

**示例**

下面的匿名代码块创建了名称为job的表。需要注意的是DDL语句是由存储过程PARSE立即执行，不要求单独运行函数EXECUTE这个步骤。

``` {#codeblock_1rq_lur_yva}
DECLARE
    curid           INTEGER;
BEGIN
    curid := DBMS_SQL.OPEN_CURSOR;
    DBMS_SQL.PARSE(curid, 'CREATE TABLE job (jobno NUMBER(3), ' ||
        'jname VARCHAR2(9))',DBMS_SQL.native);
    DBMS_SQL.CLOSE_CURSOR(curid);
END;
```

下面向表job中插入两条记录。

``` {#codeblock_r4d_huk_l8d}
DECLARE
    curid           INTEGER;
    v_sql           VARCHAR2(50);
    v_status        INTEGER;
BEGIN
    curid := DBMS_SQL.OPEN_CURSOR;
    v_sql := 'INSERT INTO job VALUES (100, ''ANALYST'')';
    DBMS_SQL.PARSE(curid, v_sql, DBMS_SQL.native);
    v_status := DBMS_SQL.EXECUTE(curid);
    DBMS_OUTPUT.PUT_LINE('Number of rows processed: ' || v_status);
    v_sql := 'INSERT INTO job VALUES (200, ''CLERK'')';
    DBMS_SQL.PARSE(curid, v_sql, DBMS_SQL.native);
    v_status := DBMS_SQL.EXECUTE(curid);
    DBMS_OUTPUT.PUT_LINE('Number of rows processed: ' || v_status);
    DBMS_SQL.CLOSE_CURSOR(curid);
END;

Number of rows processed: 1
Number of rows processed: 1
```

下面的匿名代码块使用包DBMS\_SQL执行了包含2条INSERT语句的代码块。需要注意的是在代码块结束的地方包含一个分号结束符，而在前面的一个示例中，每个单独的INSERT语句没有分号结束符。

``` {#codeblock_wg2_7s0_4ck}
DECLARE
    curid           INTEGER;
    v_sql           VARCHAR2(100);
    v_status        INTEGER;
BEGIN
    curid := DBMS_SQL.OPEN_CURSOR;
    v_sql := 'BEGIN ' ||
               'INSERT INTO job VALUES (300, ''MANAGER''); '  ||
               'INSERT INTO job VALUES (400, ''SALESMAN''); ' ||
             'END;';
    DBMS_SQL.PARSE(curid, v_sql, DBMS_SQL.native);
    v_status := DBMS_SQL.EXECUTE(curid);
    DBMS_SQL.CLOSE_CURSOR(curid);
END;
```

