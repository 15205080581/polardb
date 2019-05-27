# DBMS\_ALERT {#concept_221973 .concept}

DBMS\_ALERT包提供了注册，发送和接收告警的能力。

|Function/Procedure|Return Type|Description|
|------------------|-----------|-----------|
|REGISTER\(name\)|n/a|Register to be able to receive alerts named, name.|
|REMOVE\(name\)|n/a|Remove registration for the alert named, name.|
|REMOVEALL|n/a|Remove registration for all alerts.|
|SIGNAL\(name, message\)|n/a|Signals the alert named, name, with message.|
|WAITANY\(name OUT, message OUT, status OUT, timeout\)|n/a|Wait for any registered alert to occur.|
|WAITONE\(name, message OUT, status OUT, timeout\)|n/a|Wait for the specified alert, name, to occur.|

当与Oracle版本的DBMS\_ALERT执行对比时，POLARDB for Oracle的DBMS\_ALERT执行就是一个部分执行。POLARDB for Oracle仅支持在上述表中列出的函数和存储过程。

POLARDB for Oracle所允许的最大并发告警为5 00。我们可以使用dbms\_alert.max\_alerts GUC变量（位于postgresql.conf文件中）来指定系统允许的最大并发告警数量。

要给dbms\_alert.max\_alerts设置一个值，可使用我们自己的编辑器打开postgresql.conf文件（由缺省定位在/opt/PostgresPlus/9. 3AS/data路径中\)，然后按照下面的示例编辑dbms\_alert.max\_alerts参数：

``` {#codeblock_u8p_zjh_dn9}
dbms alert.max alerts = alert count
```

**说明：** alert\_count用于指定告警的最大并发数量。通过缺省来指定dbms\_alert.max\_alerts的值为100。如要禁用这个功能特性，可指定dbms alert.max alerts的值为0。

为了让dbms\_alert.max\_alerts GUC正确工作，custom\_variable\_classes参数必须包含dbms\_alerts：

``` {#codeblock_nt9_81t_zo3}
custom variable classes = 'dbms alert, ...'
```

在编辑postgresql.conf文件参数后，我们必须重启服务器使做的改变生效。

## REGISTER {#section_nrs_ocv_4wt .section}

存储过程REGISTER使当前会话可接收指定的告警。

**语法**

``` {#codeblock_xaf_p00_p31}
REGISTER(name VARCHAR2) 
```

**参数**

|参数名称|描述|
|----|--|
|name|被注册的告警名称。|

**示例**

下面这个匿名代码块注册了一个名为alert\_test的告警，然后等待告警信号的发生。

``` {#codeblock_41n_3vs_0a5}
DECLARE
    v_name           VARCHAR2(30) := 'alert_test';
    v_msg            VARCHAR2(80);
    v_status         INTEGER;
    v_timeout        NUMBER(3) := 120;
BEGIN
    DBMS_ALERT.REGISTER(v_name);
    DBMS_OUTPUT.PUT_LINE('Registered for alert ' || v_name);
    DBMS_OUTPUT.PUT_LINE('Waiting for signal...');
    DBMS_ALERT.WAITONE(v_name,v_msg,v_status,v_timeout);
    DBMS_OUTPUT.PUT_LINE('Alert name   : ' || v_name);
    DBMS_OUTPUT.PUT_LINE('Alert msg    : ' || v_msg);
    DBMS_OUTPUT.PUT_LINE('Alert status : ' || v_status);
    DBMS_OUTPUT.PUT_LINE('Alert timeout: ' || v_timeout || ' seconds');
    DBMS_ALERT.REMOVE(v_name);
END;

Registered for alert alert_test
Waiting for signal...
```

## REMOVE {#section_mzz_xq5_drh .section}

存储过程REMOVE为会话取消对告警的注册。

**语法**

``` {#codeblock_y2s_dzs_0d1}
REMOVE(name VARCHAR2)
```

**参数**

|参数名称|描述|
|----|--|
|name|被取消注册的告警名称。|

## REMOVEALL {#section_1bt_dcy_evf .section}

存储过程REMOVEALL为会话取消所有的告警注册。

**语法**

``` {#codeblock_izd_ggt_7q2}
REMOVEALL
```

## SIGNAL {#section_xo6_m7o_etn .section}

存储过程SIGNAL发出信号表示指定名称的告警出现。

**语法**

``` {#codeblock_zni_3wl_awx}
SIGNAL(name VARCHAR2, message VARCHAR2)
```

**参数**

|参数名称|描述|
|----|--|
|name|告警的名称。|
|message|所传递带有告警的信息。|

**示例**

下面的匿名代码块发送了名称为alert\_test的告警。

``` {#codeblock_yhp_as2_hj6}
DECLARE
    v_name   VARCHAR2(30) := 'alert_test';
BEGIN
    DBMS_ALERT.SIGNAL(v_name,'This is the message from ' || v_name);
    DBMS_OUTPUT.PUT_LINE('Issued alert for ' || v_name);
END;

Issued alert for alert_test    
```

## WAITANY {#section_jsm_vpn_9l5 .section}

存储过程WAITANY等待已注册的告警发生。

**语法**

``` {#codeblock_9uf_2vt_ecm}
WAITANY(name OUT VARCHAR2, message OUT VARCHAR2, status OUT INTEGER, timeout NUMBER)
```

**参数**

|参数名称|描述|
|----|--|
|name|接收告警名称的变量。|
|message|接收由存储过程SIGNAL所发送消息的变量。|
|status|由操作返回的状态代码。可出现的值：0 - 发生告警； 1 - 出现超时。|
|timeout|等待告警的时间，以秒为单位。|

**示例**

下面的匿名代码块使用存储过程WAITANY来接收命名为alert\_test或any\_alert的告警：

``` {#codeblock_z43_3um_9gn}
DECLARE
    v_name           VARCHAR2(30);
    v_msg            VARCHAR2(80);
    v_status         INTEGER;
    v_timeout        NUMBER(3) := 120;
BEGIN
    DBMS_ALERT.REGISTER('alert_test');
    DBMS_ALERT.REGISTER('any_alert');
    DBMS_OUTPUT.PUT_LINE('Registered for alert alert_test and any_alert');
    DBMS_OUTPUT.PUT_LINE('Waiting for signal...');
    DBMS_ALERT.WAITANY(v_name,v_msg,v_status,v_timeout);
    DBMS_OUTPUT.PUT_LINE('Alert name   : ' || v_name);
    DBMS_OUTPUT.PUT_LINE('Alert msg    : ' || v_msg);
    DBMS_OUTPUT.PUT_LINE('Alert status : ' || v_status);
    DBMS_OUTPUT.PUT_LINE('Alert timeout: ' || v_timeout || ' seconds');
    DBMS_ALERT.REMOVEALL;
END;

Registered for alert alert_test and any_alert
Waiting for signal...        
```

在第二个会话中的匿名代码块为名为any\_alert的告警发出信号：

``` {#codeblock_s6e_st0_wd4}
DECLARE
    v_name   VARCHAR2(30) := 'any_alert';
BEGIN
    DBMS_ALERT.SIGNAL(v_name,'This is the message from ' || v_name);
    DBMS_OUTPUT.PUT_LINE('Issued alert for ' || v_name);
END;

Issued alert for any_alert
```

然后控制流程返回第一个匿名代码块，然后执行剩余的代码：

``` {#codeblock_yyz_5un_x36}
Registered for alert alert_test and any_alert
Waiting for signal...
Alert name   : any_alert
Alert msg    : This is the message from any_alert
Alert status : 0
Alert timeout: 120 seconds
```

## WAITONE {#section_n0c_6wo_af5 .section}

存储过程WAITONE等待特定的注册告警发生。

**语法**

``` {#codeblock_1qs_ce1_ivr}
WAITONE(name VARCHAR2, message OUT VARCHAR2, status OUT INTEGER, timeout NUMBER)
```

**参数**

|参数名称|描述|
|----|--|
|name|告警的名称。|
|message|接收存储过程SIGNAL发送消息的变量。|
|status|由操作返回的状态代码。允许的值包括： 0 - 发生告警； 1 - 发生超时。|
|timeout|等待告警发生的时间，以秒为单位。|

**示例**

在下面的匿名代码块中，除了使用存储过程WAITONE接收名称为alert\_test的告警外，其余的地方和使用存储过程WAITANY的示例类似。

``` {#codeblock_58i_35y_bxp}
DECLARE
    v_name           VARCHAR2(30) := 'alert_test';
    v_msg            VARCHAR2(80);
    v_status         INTEGER;
    v_timeout        NUMBER(3) := 120;
BEGIN
    DBMS_ALERT.REGISTER(v_name);
    DBMS_OUTPUT.PUT_LINE('Registered for alert ' || v_name);
    DBMS_OUTPUT.PUT_LINE('Waiting for signal...');
    DBMS_ALERT.WAITONE(v_name,v_msg,v_status,v_timeout);
    DBMS_OUTPUT.PUT_LINE('Alert name   : ' || v_name);
    DBMS_OUTPUT.PUT_LINE('Alert msg    : ' || v_msg);
    DBMS_OUTPUT.PUT_LINE('Alert status : ' || v_status);
    DBMS_OUTPUT.PUT_LINE('Alert timeout: ' || v_timeout || ' seconds');
    DBMS_ALERT.REMOVE(v_name);
END;

Registered for alert alert_test
Waiting for signal...
```

在第二个会话中的一个匿名块发送名称alert\_test的告警信号：

``` {#codeblock_kny_s91_9v4}
DECLARE
    v_name   VARCHAR2(30) := 'alert_test';
BEGIN
    DBMS_ALERT.SIGNAL(v_name,'This is the message from ' || v_name);
    DBMS_OUTPUT.PUT_LINE('Issued alert for ' || v_name);
END;

Issued alert for alert_test
```

第一个会话收到告警信息，控制流程返回到匿名代码块，然后执行这个匿名代码块的剩余代码。

``` {#codeblock_oz6_k0d_51m}
Registered for alert alert_test
Waiting for signal...
Alert name   : alert_test
Alert msg    : This is the message from alert_test
Alert status : 0
Alert timeout: 120 seconds
```

## 综合性示例 {#section_m2q_012_7ci .section}

在下面的示例中，当的表dept和emp发生改变的时候，我们使用两个触发器发送告警信息。使用一个匿名代码块监听这些告警，并且当收到告警的时候，显示相关信息。

下面是表dept和emp上定义的触发器：

``` {#codeblock_6fb_wne_56h}
CREATE OR REPLACE TRIGGER dept_alert_trig
    AFTER INSERT OR UPDATE OR DELETE ON dept
DECLARE
    v_action        VARCHAR2(25);
BEGIN
    IF INSERTING THEN
        v_action := ' added department(s) ';
    ELSIF UPDATING THEN
        v_action := ' updated department(s) ';
    ELSIF DELETING THEN
        v_action := ' deleted department(s) ';
    END IF;
    DBMS_ALERT.SIGNAL('dept_alert',USER || v_action || 'on ' ||
        SYSDATE);
END;

CREATE OR REPLACE TRIGGER emp_alert_trig
    AFTER INSERT OR UPDATE OR DELETE ON emp
DECLARE
    v_action        VARCHAR2(25);
BEGIN
    IF INSERTING THEN
        v_action := ' added employee(s) ';
    ELSIF UPDATING THEN
        v_action := ' updated employee(s) ';
    ELSIF DELETING THEN
        v_action := ' deleted employee(s) ';
    END IF;
    DBMS_ALERT.SIGNAL('emp_alert',USER || v_action || 'on ' ||
        SYSDATE);
END;
```

当在其它会话中对表dept和emp进行更新操作时，在一个会话中执行下面这个匿名代码块：

``` {#codeblock_am2_3cs_ugr}
DECLARE
    v_dept_alert     VARCHAR2(30) := 'dept_alert';
    v_emp_alert      VARCHAR2(30) := 'emp_alert';
    v_name           VARCHAR2(30);
    v_msg            VARCHAR2(80);
    v_status         INTEGER;
    v_timeout        NUMBER(3) := 60;
BEGIN
    DBMS_ALERT.REGISTER(v_dept_alert);
    DBMS_ALERT.REGISTER(v_emp_alert);
    DBMS_OUTPUT.PUT_LINE('Registered for alerts dept_alert and emp_alert');
    DBMS_OUTPUT.PUT_LINE('Waiting for signal...');
    LOOP
        DBMS_ALERT.WAITANY(v_name,v_msg,v_status,v_timeout);
        EXIT WHEN v_status != 0;
        DBMS_OUTPUT.PUT_LINE('Alert name   : ' || v_name);
        DBMS_OUTPUT.PUT_LINE('Alert msg    : ' || v_msg);
        DBMS_OUTPUT.PUT_LINE('Alert status : ' || v_status);
        DBMS_OUTPUT.PUT_LINE('------------------------------------' ||
            '-------------------------');
    END LOOP;
    DBMS_OUTPUT.PUT_LINE('Alert status : ' || v_status);
    DBMS_ALERT.REMOVEALL;
END;

Registered for alerts dept_alert and emp_alert
Waiting for signal...
```

用户mary对表dept进行下面这些数据更新操作：

``` {#codeblock_y1z_pz3_gi0}
INSERT INTO dept VALUES (50,'FINANCE,,,CHICAG0');
INSERT INTO emp (empno,ename,deptno) VALUES (9001,'J0NES',50);
INSERT INTO emp (empno,ename,deptno) VALUES (9002,'ALICE',50);
			
```

用户john对表dept进行下面这些更新操作：

``` {#codeblock_byg_zom_0ee}
INSERT INTO dept VALUES (60,'HR','L0S ANGELES');
```

下面这些是从触发器中接收告警信号的匿名代码块所显示的输出：

``` {#codeblock_21c_c1t_map}
Registered for alerts dept_alert and emp_alert
Waiting for signal...
Alert name   : dept_alert
Alert msg    : mary added department(s) on 25-OCT-07 16:41:01
Alert status : 0
-------------------------------------------------------------
Alert name   : emp_alert
Alert msg    : mary added employee(s) on 25-OCT-07 16:41:02
Alert status : 0
-------------------------------------------------------------
Alert name   : dept_alert
Alert msg    : john added department(s) on 25-OCT-07 16:41:22
Alert status : 0
-------------------------------------------------------------
Alert status : 1
```

