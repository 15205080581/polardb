# DBMS\_OUTPUT {#concept_221982 .concept}

包DBMS\_OUTPUT 用于向消息缓冲区发送消息（文本行的形式出现），或者从消息缓冲区中获取消息。消息缓冲区是属于单独会话的一部分。我们可以使用包DBMS\_PIPE在会话之间传送信息。

下面的表中列出了在包DBMS\_OUTPUT中允许使用的存储过程和函数。

|Function/Procedure|Return Type|Description|
|------------------|-----------|-----------|
|DISABLE|n/a|Disable the capability to send and receive messages.|
|ENABLE\(buffer size\)|n/a|Enable the capability to send and receive messages.|
|GET LINE\(line OUT, status OUT\)|n/a|Get a line from the message buffer.|
|GET LINES\(lines OUT, numlines IN OUT\)|n/a|Get multiple lines from the message buffer.|
|NEW LINE|n/a|Puts an end-of-line character sequence.|
|PUT\(item\)|n/a|Puts a partial line without an end-of-line character sequence.|
|PUT LINE\(item\)|n/a|Puts a complete line with an end-of-line character sequence.|
|SERVEROUTPUT\(stdout\)|n/a|Direct messages from PUT, PUT LINE, or NEW\_LINE to either standard output or the message buffer.|

下面的表格列出了包DBMS\_OUTPUT中允许使用的公有变量。

|Public Variables|Data Type|Value|Description|
|----------------|---------|-----|-----------|
|chararr|TABLE| |For message lines.|

## CHARARR {#section_h9z_9tg_2nx .section}

变量CHARARR用于存储多行消息文本。

``` {#codeblock_mju_d97_02v}
TYPE chararr IS TABLE OF VARCHAR2(32767) INDEX BY BINARY_INTEGER;
```

## DISABLE {#section_z6y_u1g_ed0 .section}

存储过程DISABLE用于清空消息缓冲区。在执行存储过程DISABLE时, 将不能再访问任何在缓冲区 中的消息。任何随后由PUT, PUT\_LINE, 或者NEW\_LINE发送的消息将被放弃。当存储过程PUT, PUT\_LINE, 或者是NEW\_LINE执行的时候，没有错误返回，并且缓冲区中消息变成无效状态。

我们可以使用存储过程ENABLE或SERVEROUTPUT\(TRUE\)来重新使发送和接收消息有效。

``` {#codeblock_tci_68g_wd2}
DISABLE
```

**示例**

下面的匿名代码块禁止在当前会话中发送和接收消息。

``` {#codeblock_nfz_v5q_oc0}
BEGIN
    DBMS_OUTPUT.DISABLE;
END;
```

## ENABLE {#section_dlp_h3j_ro0 .section}

存储过程ENABLE使向消息缓冲区发送消息，或从消息缓冲区中接收消息的功能生效。当运行存储 过程SERVEROUTPUT\(TRUE\)时，同时也在隐含状态下执行存储过程ENABLE。

SERVEROUTPUT的状态决定了PUT,PUT\_LINE或NEW\_LINE发送消息的目的地。

-   如果SERVEROUTPUT的最新状态是”true”，那么把消息送到命令行的标准输出中。
-   如果SERVEROUTPUT的最新状态是”false”，那么把消息送到消息缓冲区中。

``` {#codeblock_ynp_5cf_4ki}
ENABLE [ (buffer_size INTEGER) ]
```

**参数**

|参数名称|描述|
|----|--|
|buffer size|消息缓冲区的最大长度，以字节为单位。如果指定的buffer\_size小于2000,那么会自动把它设为2000。|

**示例**

下面的匿名代码块使消息传递的功能生效。通过设置SERVEROUTPUT（TRUE），可以强制把消息送到标准输出中。

``` {#codeblock_hy9_fm3_ea7}
BEGIN
    DBMS_OUTPUT.ENABLE;
    DBMS_OUTPUT.SERVEROUTPUT(TRUE);
    DBMS_OUTPUT.PUT_LINE('Messages enabled');
END;

Messages enabled
```

我们也可以只通过使用SERVEROUTPUT\(TRUE\)，来实现相同的效果。

``` {#codeblock_6bn_2r2_5mp}
BEGIN
    DBMS_OUTPUT.SERVEROUTPUT(TRUE);
    DBMS_OUTPUT.PUT_LINE('Messages enabled');
END;

Messages enabled
```

下面的匿名代码块阻止消息传递功能，但是通过设置SERVEROUTPUT\(FALSE\)，将消息送到消息 缓冲区中。

``` {#codeblock_juh_sgw_lu6}
BEGIN
    DBMS_OUTPUT.ENABLE;
    DBMS_OUTPUT.SERVEROUTPUT(FALSE);
    DBMS_OUTPUT.PUT_LINE('Message sent to buffer');
END;
```

## GET\_LINE {#section_4dq_p0f_vms .section}

通过使用存储过程GET\_LINE，我们可以从消息缓冲区中获取一行文本。我们只能获取由行结束符 终止的文本-这是通过使用函数PUT\_LINE，或者在调用NEW\_LINE后，执行的一系列PUT函数的调 用来产生的完整文本行。

``` {#codeblock_0nb_5qw_bnj}
GET_LINE(line OUT VARCHAR2, status OUT INTEGER)
```

**参数**

|参数名称|描述|
|----|--|
|line|用于从消息缓冲区接收文本行的变量。|
|status|如果一行文本从消息缓冲区返回，那么为0。如果没有文本返回，那么返回为1。|

**示例**

在下面的匿名代码块中，把表emp中每条记录以逗号分隔的字符串形式写到消息缓冲区中。

``` {#codeblock_h6f_9ti_cau}
EXEC DBMS_OUTPUT.SERVEROUTPUT(FALSE);

DECLARE
    v_emprec        VARCHAR2(120);
    CURSOR emp_cur IS SELECT * FROM emp ORDER BY empno;
BEGIN
    DBMS_OUTPUT.ENABLE;
    FOR i IN emp_cur LOOP
        v_emprec := i.empno || ',' || i.ename || ',' || i.job || ',' ||
            NVL(LTRIM(TO_CHAR(i.mgr,'9999')),'') || ',' || i.hiredate ||
            ',' || i.sal || ',' ||
            NVL(LTRIM(TO_CHAR(i.comm,'9990.99')),'') || ',' || i.deptno;
        DBMS_OUTPUT.PUT_LINE(v_emprec);
    END LOOP;
END;
```

在下面的匿名代码块中，首先从消息缓冲区中读取文本消息，然后把前一个示例写入的消息写入到名为messages的表中，然后显示消息中的记录。

``` {#codeblock_etc_98t_4x3}
CREATE TABLE messages (
    status          INTEGER,
    msg             VARCHAR2(100)
);

DECLARE
    v_line          VARCHAR2(100);
    v_status        INTEGER := 0;
BEGIN
    DBMS_OUTPUT.GET_LINE(v_line,v_status);
    WHILE v_status = 0 LOOP
        INSERT INTO messages VALUES(v_status, v_line);
        DBMS_OUTPUT.GET_LINE(v_line,v_status);
    END LOOP;
END;

SELECT msg FROM messages;

                               msg
-----------------------------------------------------------------
 7369,SMITH,CLERK,7902,17-DEC-80 00:00:00,800.00,,20
 7499,ALLEN,SALESMAN,7698,20-FEB-81 00:00:00,1600.00,300.00,30
 7521,WARD,SALESMAN,7698,22-FEB-81 00:00:00,1250.00,500.00,30
 7566,JONES,MANAGER,7839,02-APR-81 00:00:00,2975.00,,20
 7654,MARTIN,SALESMAN,7698,28-SEP-81 00:00:00,1250.00,1400.00,30
 7698,BLAKE,MANAGER,7839,01-MAY-81 00:00:00,2850.00,,30
 7782,CLARK,MANAGER,7839,09-JUN-81 00:00:00,2450.00,,10
 7788,SCOTT,ANALYST,7566,19-APR-87 00:00:00,3000.00,,20
 7839,KING,PRESIDENT,,17-NOV-81 00:00:00,5000.00,,10
 7844,TURNER,SALESMAN,7698,08-SEP-81 00:00:00,1500.00,0.00,30
 7876,ADAMS,CLERK,7788,23-MAY-87 00:00:00,1100.00,,20
 7900,JAMES,CLERK,7698,03-DEC-81 00:00:00,950.00,,30
 7902,FORD,ANALYST,7566,03-DEC-81 00:00:00,3000.00,,20
 7934,MILLER,CLERK,7782,23-JAN-82 00:00:00,1300.00,,10
(14 rows)
```

## GET\_LINES {#section_skd_fkg_kk4 .section}

我们可以使用存储过程GET\_LINES从消息缓冲区中获取多行文本，然后把这些文本放到一个集合 中。只有以行结束符终止的文本才能被取出来-这是通过使用函数PUT\_LINE，或者在调用NEW\_LINE 后，执行一系列PUT函数的调用来产生的完整文本行。

``` {#codeblock_pkt_ee4_hls}
GET_LINES(lines OUT CHARARR, numlines IN OUT INTEGER)
```

**参数**

|参数名称|描述|
|----|--|
|lines|从消息缓冲区中接收文本行的表。关于lines的描述，参见变量CHARARR 。|
|numlines IN|从消息缓冲区中取出的文本行数。|
|numlines OUT|从消息缓冲区中实际取出的文本行数量。如果numlines的输出值小于输入值，那么表示在消息缓冲区中，没有文本了。|

**示例**

在下面的示例中，我们使用存储过程GET\_LINES将放在消息缓冲区中表emp的记录存放到一个数组 中。

``` {#codeblock_ptq_uem_19o}
EXEC DBMS_OUTPUT.SERVEROUTPUT(FALSE);

DECLARE
    v_emprec        VARCHAR2(120);
    CURSOR emp_cur IS SELECT * FROM emp ORDER BY empno;
BEGIN
    DBMS_OUTPUT.ENABLE;
    FOR i IN emp_cur LOOP
        v_emprec := i.empno || ',' || i.ename || ',' || i.job || ',' ||
            NVL(LTRIM(TO_CHAR(i.mgr,'9999')),'') || ',' || i.hiredate ||
            ',' || i.sal || ',' ||
            NVL(LTRIM(TO_CHAR(i.comm,'9990.99')),'') || ',' || i.deptno;
        DBMS_OUTPUT.PUT_LINE(v_emprec);
    END LOOP;
END;

DECLARE
    v_lines         DBMS_OUTPUT.CHARARR;
    v_numlines      INTEGER := 14;
    v_status        INTEGER := 0;
BEGIN
    DBMS_OUTPUT.GET_LINES(v_lines,v_numlines);
    FOR i IN 1..v_numlines LOOP
        INSERT INTO messages VALUES(v_numlines, v_lines(i));
    END LOOP;
END;

SELECT msg FROM messages;

                               msg
-----------------------------------------------------------------
 7369,SMITH,CLERK,7902,17-DEC-80 00:00:00,800.00,,20
 7499,ALLEN,SALESMAN,7698,20-FEB-81 00:00:00,1600.00,300.00,30
 7521,WARD,SALESMAN,7698,22-FEB-81 00:00:00,1250.00,500.00,30
 7566,JONES,MANAGER,7839,02-APR-81 00:00:00,2975.00,,20
 7654,MARTIN,SALESMAN,7698,28-SEP-81 00:00:00,1250.00,1400.00,30
 7698,BLAKE,MANAGER,7839,01-MAY-81 00:00:00,2850.00,,30
 7782,CLARK,MANAGER,7839,09-JUN-81 00:00:00,2450.00,,10
 7788,SCOTT,ANALYST,7566,19-APR-87 00:00:00,3000.00,,20
 7839,KING,PRESIDENT,,17-NOV-81 00:00:00,5000.00,,10
 7844,TURNER,SALESMAN,7698,08-SEP-81 00:00:00,1500.00,0.00,30
 7876,ADAMS,CLERK,7788,23-MAY-87 00:00:00,1100.00,,20
 7900,JAMES,CLERK,7698,03-DEC-81 00:00:00,950.00,,30
 7902,FORD,ANALYST,7566,03-DEC-81 00:00:00,3000.00,,20
 7934,MILLER,CLERK,7782,23-JAN-82 00:00:00,1300.00,,10
(14 rows)
```

## NEW LINE {#section_5d1_ijk_cgc .section}

存储过程NEW\_LINE在消息缓冲区中写入一个行结束符。

``` {#codeblock_11v_6fd_uuz}
NEW_LINE
```

**参数**

NEW\_LINE 存储过程不需要参数。

## PUT {#section_hdz_eno_t2c .section}

存储过程PUT将一个字符串写到消息缓冲区中。它不写入在这个字符串结尾的行结束符。我们可以 使用存储过程NEW\_LINE增加一个行结束符。

``` {#codeblock_9c1_126_bgq}
PUT(item VARCHAR2)
```

**参数**

|参数名称|描述|
|----|--|
|item|写到消息缓冲区中文本。|

**示例**

下面的示例使用存储过程PUT显示了从表emp中查询出的雇员信息列表，这些雇员信息是以以逗号分隔方式展现的。

``` {#codeblock_max_oq9_vhy}
DECLARE
    CURSOR emp_cur IS SELECT * FROM emp ORDER BY empno;
BEGIN
    FOR i IN emp_cur LOOP
        DBMS_OUTPUT.PUT(i.empno);
        DBMS_OUTPUT.PUT(',');
        DBMS_OUTPUT.PUT(i.ename);
        DBMS_OUTPUT.PUT(',');
        DBMS_OUTPUT.PUT(i.job);
        DBMS_OUTPUT.PUT(',');
        DBMS_OUTPUT.PUT(i.mgr);
        DBMS_OUTPUT.PUT(',');
        DBMS_OUTPUT.PUT(i.hiredate);
        DBMS_OUTPUT.PUT(',');
        DBMS_OUTPUT.PUT(i.sal);
        DBMS_OUTPUT.PUT(',');
        DBMS_OUTPUT.PUT(i.comm);
        DBMS_OUTPUT.PUT(',');
        DBMS_OUTPUT.PUT(i.deptno);
        DBMS_OUTPUT.NEW_LINE;
    END LOOP;
END;

7369,SMITH,CLERK,7902,17-DEC-80 00:00:00,800.00,,20
7499,ALLEN,SALESMAN,7698,20-FEB-81 00:00:00,1600.00,300.00,30
7521,WARD,SALESMAN,7698,22-FEB-81 00:00:00,1250.00,500.00,30
7566,JONES,MANAGER,7839,02-APR-81 00:00:00,2975.00,,20
7654,MARTIN,SALESMAN,7698,28-SEP-81 00:00:00,1250.00,1400.00,30
7698,BLAKE,MANAGER,7839,01-MAY-81 00:00:00,2850.00,,30
7782,CLARK,MANAGER,7839,09-JUN-81 00:00:00,2450.00,,10
7788,SCOTT,ANALYST,7566,19-APR-87 00:00:00,3000.00,,20
7839,KING,PRESIDENT,,17-NOV-81 00:00:00,5000.00,,10
7844,TURNER,SALESMAN,7698,08-SEP-81 00:00:00,1500.00,0.00,30
7876,ADAMS,CLERK,7788,23-MAY-87 00:00:00,1100.00,,20
7900,JAMES,CLERK,7698,03-DEC-81 00:00:00,950.00,,30
7902,FORD,ANALYST,7566,03-DEC-81 00:00:00,3000.00,,20
7934,MILLER,CLERK,7782,23-JAN-82 00:00:00,1300.00,,10
```

## PUT\_LINE {#section_w4c_jo5_kgt .section}

存储过程PUT\_LINE向消息缓冲区写入一行带有行结束符的文本。

``` {#codeblock_jjm_nq0_bgl}
PUT_LINE(item VARCHAR2)
```

**参数**

|参数名称|描述|
|----|--|
|item|写入消息缓冲区的文本。|

**示例**

下面的示例使用存储过程PUT\_LINE显示了从表emp中查出的雇员记录，这些记录是以逗号分隔列 表的形式展现的。

``` {#codeblock_5l5_0fv_3if}
DECLARE
    v_emprec        VARCHAR2(120);
    CURSOR emp_cur IS SELECT * FROM emp ORDER BY empno;
BEGIN
    FOR i IN emp_cur LOOP
        v_emprec := i.empno || ',' || i.ename || ',' || i.job || ',' ||
            NVL(LTRIM(TO_CHAR(i.mgr,'9999')),'') || ',' || i.hiredate ||
            ',' || i.sal || ',' ||
            NVL(LTRIM(TO_CHAR(i.comm,'9990.99')),'') || ',' || i.deptno;
        DBMS_OUTPUT.PUT_LINE(v_emprec);
    END LOOP;
END;

7369,SMITH,CLERK,7902,17-DEC-80 00:00:00,800.00,,20
7499,ALLEN,SALESMAN,7698,20-FEB-81 00:00:00,1600.00,300.00,30
7521,WARD,SALESMAN,7698,22-FEB-81 00:00:00,1250.00,500.00,30
7566,JONES,MANAGER,7839,02-APR-81 00:00:00,2975.00,,20
7654,MARTIN,SALESMAN,7698,28-SEP-81 00:00:00,1250.00,1400.00,30
7698,BLAKE,MANAGER,7839,01-MAY-81 00:00:00,2850.00,,30
7782,CLARK,MANAGER,7839,09-JUN-81 00:00:00,2450.00,,10
7788,SCOTT,ANALYST,7566,19-APR-87 00:00:00,3000.00,,20
7839,KING,PRESIDENT,,17-NOV-81 00:00:00,5000.00,,10
7844,TURNER,SALESMAN,7698,08-SEP-81 00:00:00,1500.00,0.00,30
7876,ADAMS,CLERK,7788,23-MAY-87 00:00:00,1100.00,,20
7900,JAMES,CLERK,7698,03-DEC-81 00:00:00,950.00,,30
7902,FORD,ANALYST,7566,03-DEC-81 00:00:00,3000.00,,20
7934,MILLER,CLERK,7782,23-JAN-82 00:00:00,1300.00,,10
```

## SERVEROUTPUT {#section_in6_s5w_x7f .section}

存储过程SERVEROUTPUT提供了将消息指向命令行的标准输出或消息缓冲区的功能。通过设置 SERVEROUTPUT\(TRUE\)，能够在隐含状态下执行存储过程ENABLE。

SERVEROUTPUT的缺省设置取决于实际应用。例如，在Oracle的SQL\*PLUS中，SERVEROUTPUT\(FALSE\)是缺省设置。在PSQL中，SERVEROUTPUT\(TRUE\)是缺省设置。同时也要注意的是，在OracleSQL\*PLUS中，这个设置是通过使用SQL\*PLus的SET命令来控制的，而不是如在POLARDB for Oracle中那样，由存储过程来实现。

``` {#codeblock_i66_xhp_0x6}
SERVEROUTPUT(stdout BOOLEAN)
```

**参数**

|参数名称|描述|
|----|--|
|stdout|如果随后的PUT,PUT\_LINE,或者NEW\_LINE命令要把文本直接送到命令行的标准输出中，那么把这个参数设为”true”。如果把文本送到消息缓冲区中，那么把这个值设为”false”。|

**示例**

下面的匿名块把第一条信息发送到命令行的标准输出，把第二条信息发送到消息缓冲区。

``` {#codeblock_wnl_u16_bzd}
BEGIN
    DBMS_OUTPUT.SERVEROUTPUT(TRUE);
    DBMS_OUTPUT.PUT_LINE('This message goes to the command line');
    DBMS_OUTPUT.SERVEROUTPUT(FALSE);
    DBMS_OUTPUT.PUT_LINE('This message goes to the message buffer');
END;

This message goes to the command line
```

如果在同一个会话中执行下面的匿名代码块，那么就会把在前面示例中存放在消息缓冲区的消息强制清洗，并且做为一条新的信息在命令行上显示出来。

``` {#codeblock_xtm_5pj_wa5}
BEGIN
    DBMS_OUTPUT.SERVEROUTPUT(TRUE);
    DBMS_OUTPUT.PUT_LINE('Flush messages from the buffer');
END;

This message goes to the message buffer
Flush messages from the buffer
```

