# DBMS\_PIPE {#concept_221983 .concept}

我们可以使用包DBMS\_PIPE通过一个管道在连接到相同数据库集群的会话内部或者会话之间来传 递消息。

下面的表列出了在包DBMS\_PIPE中允许使用的存储过程和函数。

|Function/Procedure|Return Type|Description|
|------------------|-----------|-----------|
|CREATE PIPE\(pipename \[, maxpipesize \] \[, private \]\)|INTEGER|Explicitly create a private pipe if private is "true" \(the default\) or a public pipe if private is "false".|
|NEXT ITEM TYPE|INTEGER|Determine the data type of the next item in a received message.|
|PACK MESSAGE\(item\)|n/a|Place item in the session's local message buffer.|
|PURGE\(pipename\)|n/a|Remove unreceived messages from the specified pipe.|
|RECEIVE MESSAGE\(pipename \[, timeout \]\)|INTEGER|Get a message from a specified pipe.|
|REMOVE PIPE\(pipename\)|INTEGER|Delete an explicitly created pipe.|
|RESET BUFFER|n/a|Reset the local message buffer.|
|SEND MESSAGE\(pipename \[, timeout \] \[, maxpipesize \]\)|INTEGER|Send a message on a pipe.|
|UNIQUE SESSION NAME|VARCHAR2|Obtain a unique session name.|
|UNPACK MESSAGE\(item OUT\)|n/a|Retrieve the next data item from a message into a type-compatible variable, item.|

管道分为显式创建和隐式创建这两种。如果引用一个先前没有由函数CREATE\_PIPE创建的管道名 称，那么就会隐式地创建一个管道。例如：如果在执行函数SEND\_MESSAGE时使用了一个不存在的管道名称，那么就用这个名称隐式地创建一个管道。通过使用函数CREATE\_PIPE，并将这个函数的第一个参数指定为新管道的名称，我们可以显式地创建一个管道。

我们也可以把管道分成私有和公有这两种。只有创建管道的用户才能访问一个私有管道，甚至超级用户都不能访问由其它用户创建的管道。而任何能够访问包DBMS\_PIPE的用户都可以访问一个公有管道。

通过将第三个参数设置为”false”，我们可以使用函数CREATE\_PIPE创建一个公有管道。而如果把 函数CREATE\_PIPE的第三个参数设置为”true”或者省略这个参数，我们就可以创建一个私有管道 。所有隐式创建的管道都是私有的。

第一次在本地消息缓冲区创建的单独数据项或者消息文本行，对于当前会话来说是唯一的。我们使用存储过程PACK\_MESSAGE在会话的本地消息缓冲区中创建消息，使用函数SEND\_MESSAGE通过管道发送消息。

而消息的接收则涉及到了相反的操作顺序，我们首先使用函数RECEIVE\_MESSAGE从指定的管道中获得消息，把消息写到会话的本地缓冲区中。然后我们使用存储过程UNPACK\_MESSAGE将消息的数据成员从消息缓冲区中传递到程序变量。如果管道包含多条消息，那么函数RECEIVE\_MESSAGE以先进先出的顺序接收消息。

对于存储过程PACK\_MESSAGE创建的消息和函数RECEIVE\_MESSAGE获取的消息来说，每一个会话为这两种消息分别保持各自不同的消息缓冲区。这样，我们可以在相同的会话中创建和接收消息。然而，如果连续执行函数RECEIVE\_MESSAGE， 那么只有最后一次执行函数RECEIVE\_MESSAGE所获取的消息保留在本地消息缓冲区中。

## CREATE\_PIPE {#section_2sp_7f1_p1u .section}

函数CREATE\_PIPE使用指定的名称显式地创建了一个公有或私有的管道。

``` {#codeblock_ikg_g2y_cu7}
status INTEGER CREATE_PIPE(pipename VARCHAR2
  [, maxpipesize INTEGER ] [, private BOOLEAN ])
```

**参数**

|参数名称|描述|
|----|--|
|pipename|管道的名称。|
|maxpipesize|管道的最大容量，以字节为单位。缺省值是8192字节。|
|private|如果创建公有管道，那么把这个参数设置为”false”. 如果创建一个私有管道，那么把这个参数设定为"true"\(这是缺省情况）。|
|status|创建管道的操作返回的状态代码。0表示成功创建。|

**示例**

创建一个名称为messages的私有管道：

``` {#codeblock_vpi_okv_i5p}
DECLARE
    v_status        INTEGER;
BEGIN
    v_status := DBMS_PIPE.CREATE_PIPE('messages');
    DBMS_OUTPUT.PUT_LINE('CREATE_PIPE status: ' || v_status);
END;
CREATE_PIPE status: 0
```

下列示例创建了一个名为mailbox的公有管道：

``` {#codeblock_qp5_44c_tqm}
DECLARE
    v_status        INTEGER;
BEGIN
    v_status := DBMS_PIPE.CREATE_PIPE('mailbox',8192,FALSE);
    DBMS_OUTPUT.PUT_LINE('CREATE_PIPE status: ' || v_status);
END;
CREATE_PIPE status: 0
```

## NEXT\_ITEM\_TYPE {#section_s9q_04k_j50 .section}

函数NEXT\_ITEM\_TYPE返回一个整数型代码，用于标识消息中下一个数据成员的数据类型，其中 消息应已经送到会话的本地缓冲区中。当我们使用存储过程UNPACK\_MESSAGE从本地消息缓冲 区移出每一个数据成员时，函数NEXT\_ITEM\_TYPE将返回下一个成员的数据类型代码。当在消息 中没有成员的时候，将返回代码。

``` {#codeblock_71f_e39_0jz}
typecode INTEGER NEXT_ITEM_TYPE
```

**参数**

|参数名称|描述|
|----|--|
|typecode|如表[表 2](#table_6zr_r0x_f4x)所示，这是一个代码，用于标识消息中下一个数据项的数据类型。|

|Type Code|Data Type|
|---------|---------|
|0|No more data items|
|9|NUMBER|
|11|VARCHAR2|
|13|DATE|
|23|RAW|

**说明：** 在表中列出的类型代码与Oracle不兼容。Oracle给数据类型分配了一个不同的编号序列。

下面的示例显示了一个管道，这个管道填充了NUMBER类型的成员，一个VARCHAR2成员，一个 DATE成员和一个RAW成员，在第二个匿名代码块中使用了函数NEXT\_ITEM\_TYPE显示每个成员 的类型代码。

``` {#codeblock_04h_f6k_kts}
DECLARE
    v_number        NUMBER := 123;
    v_varchar       VARCHAR2(20) := 'Character data';
    v_date          DATE := SYSDATE;
    v_raw           RAW(4) := '21222324';
    v_status        INTEGER;
BEGIN
    DBMS_PIPE.PACK_MESSAGE(v_number);
    DBMS_PIPE.PACK_MESSAGE(v_varchar);
    DBMS_PIPE.PACK_MESSAGE(v_date);
    DBMS_PIPE.PACK_MESSAGE(v_raw);
    v_status := DBMS_PIPE.SEND_MESSAGE('datatypes');
    DBMS_OUTPUT.PUT_LINE('SEND_MESSAGE status: ' || v_status);
EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('SQLERRM: ' || SQLERRM);
        DBMS_OUTPUT.PUT_LINE('SQLCODE: ' || SQLCODE);
END;

SEND_MESSAGE status: 0

DECLARE
    v_number        NUMBER;
    v_varchar       VARCHAR2(20);
    v_date          DATE;
    v_timestamp     TIMESTAMP;
    v_raw           RAW(4);
    v_status        INTEGER;
BEGIN
    v_status := DBMS_PIPE.RECEIVE_MESSAGE('datatypes');
    DBMS_OUTPUT.PUT_LINE('RECEIVE_MESSAGE status: ' || v_status);
    DBMS_OUTPUT.PUT_LINE('----------------------------------');

    v_status := DBMS_PIPE.NEXT_ITEM_TYPE;
    DBMS_OUTPUT.PUT_LINE('NEXT_ITEM_TYPE: ' || v_status);
    DBMS_PIPE.UNPACK_MESSAGE(v_number);
    DBMS_OUTPUT.PUT_LINE('NUMBER Item   : ' || v_number);
    DBMS_OUTPUT.PUT_LINE('----------------------------------');
    v_status := DBMS_PIPE.NEXT_ITEM_TYPE;
    DBMS_OUTPUT.PUT_LINE('NEXT_ITEM_TYPE: ' || v_status);
    DBMS_PIPE.UNPACK_MESSAGE(v_varchar);
    DBMS_OUTPUT.PUT_LINE('VARCHAR2 Item : ' || v_varchar);
    DBMS_OUTPUT.PUT_LINE('----------------------------------');

    v_status := DBMS_PIPE.NEXT_ITEM_TYPE;
    DBMS_OUTPUT.PUT_LINE('NEXT_ITEM_TYPE: ' || v_status);
    DBMS_PIPE.UNPACK_MESSAGE(v_date);
    DBMS_OUTPUT.PUT_LINE('DATE Item     : ' || v_date);
    DBMS_OUTPUT.PUT_LINE('----------------------------------');

    v_status := DBMS_PIPE.NEXT_ITEM_TYPE;
    DBMS_OUTPUT.PUT_LINE('NEXT_ITEM_TYPE: ' || v_status);
    DBMS_PIPE.UNPACK_MESSAGE(v_raw);
    DBMS_OUTPUT.PUT_LINE('RAW Item      : ' || v_raw);
    DBMS_OUTPUT.PUT_LINE('----------------------------------');

    v_status := DBMS_PIPE.NEXT_ITEM_TYPE;
    DBMS_OUTPUT.PUT_LINE('NEXT_ITEM_TYPE: ' || v_status);
    DBMS_OUTPUT.PUT_LINE('---------------------------------');
EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('SQLERRM: ' || SQLERRM);
        DBMS_OUTPUT.PUT_LINE('SQLCODE: ' || SQLCODE);
END;

RECEIVE_MESSAGE status: 0
----------------------------------
NEXT_ITEM_TYPE: 9
NUMBER Item   : 123
----------------------------------
NEXT_ITEM_TYPE: 11
VARCHAR2 Item : Character data
----------------------------------
NEXT_ITEM_TYPE: 13
DATE Item     : 02-OCT-07 11:11:43
----------------------------------
NEXT_ITEM_TYPE: 23
RAW Item      : 21222324
----------------------------------
NEXT_ITEM_TYPE: 0
```

## PACK\_MESSAGE {#section_q6h_me4_c8n .section}

存储过程PACK\_MESSAGE的作用是将一个数据项放入会话的本地消息缓冲区中。在使用函数 SEND\_MESSAGE前，必须至少执行一次函数PACK\_MESSAGE。

``` {#codeblock_a8e_240_l89}
PACK_MESSAGE(item { DATE | NUMBER | VARCHAR2 | RAW })
```

当我们使用函数RECEIVE\_MESSAGE取出消息后，使用存储过程UNPACK\_MESSAGE来获取消息 中的数据项。

**参数**

|参数名称|描述|
|----|--|
|item|一个表达式，用于计算任何可接受数据类型的参数。计算完毕后，会把结果值添加到会话的本地消息缓冲区中。|

## PURGE {#section_yms_f6s_57l .section}

存储过程PURGE从指定的隐式管道中删除未接收到的消息。

``` {#codeblock_yon_47h_kfn}
PURGE(pipename VARCHAR2)
```

通过使用函数REMOVE\_PIPE，可以删除一个显式创建的管道。

**参数**

|参数名称|描述|
|----|--|
|pipename|管道的名称。|

**示例**

在一个管道上发送两条消息：

``` {#codeblock_q4i_rrp_u0u}
DECLARE
    v_status        INTEGER;
BEGIN
    DBMS_PIPE.PACK_MESSAGE('Message #1');
    v_status := DBMS_PIPE.SEND_MESSAGE('pipe');
    DBMS_OUTPUT.PUT_LINE('SEND_MESSAGE status: ' || v_status);

    DBMS_PIPE.PACK_MESSAGE('Message #2');
    v_status := DBMS_PIPE.SEND_MESSAGE('pipe');
    DBMS_OUTPUT.PUT_LINE('SEND_MESSAGE status: ' || v_status);
END;

SEND_MESSAGE status: 0
SEND_MESSAGE status: 0
```

接收第一条消息，然后打开：

``` {#codeblock_coz_o33_e8g}
DECLARE
    v_item          VARCHAR2(80);
    v_status        INTEGER;
BEGIN
    v_status := DBMS_PIPE.RECEIVE_MESSAGE('pipe',1);
    DBMS_OUTPUT.PUT_LINE('RECEIVE_MESSAGE status: ' || v_status);
    DBMS_PIPE.UNPACK_MESSAGE(v_item);
    DBMS_OUTPUT.PUT_LINE('Item: ' || v_item);
END;

RECEIVE_MESSAGE status: 0
Item: Message #1
```

清除管道中的内容：

``` {#codeblock_a6g_1yq_32b}
EXEC DBMS_PIPE.PURGE('pipe');
```

当我们尝试取出下一条消息时，函数RECEIVE\_MESSAGE会返回状态代码1，表示超时，因为这时在管道中没有消息了。

``` {#codeblock_z92_ilb_l4t}
DECLARE
    v_item          VARCHAR2(80);
    v_status        INTEGER;
BEGIN
    v_status := DBMS_PIPE.RECEIVE_MESSAGE('pipe',1);
    DBMS_OUTPUT.PUT_LINE('RECEIVE_MESSAGE status: ' || v_status);
END;

RECEIVE_MESSAGE status: 1
```

## RECEIVE\_MESSAGE {#section_ked_xje_b1d .section}

函数RECEIVE\_MESSAGE用于从指定的管道中获取一条消息。

``` {#codeblock_pa9_nsv_vl4}
status INTEGER RECEIVE_MESSAGE(pipename VARCHAR2
  [, timeout INTEGER ])
```

**参数**

 `pipename` 

管道的名称。

 `timeout` 

等待时间（以秒为单位）。缺省是86400000（表示1000天）。

 `Status` 

由函数操作返回的状态代码。

允许使用状态代码如下：

|Status Code|Description|
|-----------|-----------|
|0|Success|
|1|Time out|
|2|Message too large .for the buffer|

## REMOVE\_PIPE {#section_1hv_rxx_zn2 .section}

函数REMOVE\_PIPE用于删除一个显式的私有或公有管道。

``` {#codeblock_0vt_xw6_ad0}
status INTEGER REMOVE_PIPE(pipename VARCHAR2)
```

我们可以使用函数REMOVE\_PIPE来删除一个显式创建的管道-例如.,使用函数CREATE\_PIPE创建的 管道。

**参数**

|参数名称|描述|
|----|--|
|pipename|管道的名称。|
|status|函数操作所返回的状态代码。即使命名的管道不存在，也会返回状态代码0。|

**示例**

在管道中发送两条消息：

``` {#codeblock_uj2_4ra_pge}
DECLARE
    v_status        INTEGER;
BEGIN
    v_status := DBMS_PIPE.CREATE_PIPE('pipe');
    DBMS_OUTPUT.PUT_LINE('CREATE_PIPE status : ' || v_status);

    DBMS_PIPE.PACK_MESSAGE('Message #1');
    v_status := DBMS_PIPE.SEND_MESSAGE('pipe');
    DBMS_OUTPUT.PUT_LINE('SEND_MESSAGE status: ' || v_status);

    DBMS_PIPE.PACK_MESSAGE('Message #2');
    v_status := DBMS_PIPE.SEND_MESSAGE('pipe');
    DBMS_OUTPUT.PUT_LINE('SEND_MESSAGE status: ' || v_status);
END;

CREATE_PIPE status : 0
SEND_MESSAGE status: 0
SEND_MESSAGE status: 0
```

接收第一条消息，然后打开：

``` {#codeblock_6a3_b7c_s6d}
DECLARE
    v_item          VARCHAR2(80);
    v_status        INTEGER;
BEGIN
    v_status := DBMS_PIPE.RECEIVE_MESSAGE('pipe',1);
    DBMS_OUTPUT.PUT_LINE('RECEIVE_MESSAGE status: ' || v_status);
    DBMS_PIPE.UNPACK_MESSAGE(v_item);
    DBMS_OUTPUT.PUT_LINE('Item: ' || v_item);
END;

RECEIVE_MESSAGE status: 0
Item: Message #1
```

删除管道：

``` {#codeblock_is3_bvu_9gd}
SELECT DBMS_PIPE.REMOVE_PIPE('pipe') FROM DUAL;

remove_pipe
-------------
           0
(1 row)
```

当我们尝试取回下一条消息，函数RECEIVE\_MESSAGE 将返回状态代码1，表示超时，这是因为 已经把管道删除了。

``` {#codeblock_5u9_z70_dav}
DECLARE
    v_item          VARCHAR2(80);
    v_status        INTEGER;
BEGIN
    v_status := DBMS_PIPE.RECEIVE_MESSAGE('pipe',1);
    DBMS_OUTPUT.PUT_LINE('RECEIVE_MESSAGE status: ' || v_status);
END;

RECEIVE_MESSAGE status: 1
```

## RESET\_BUFFER {#section_bmu_hnh_yw2 .section}

存储过程RESET\_BUFFER将会话的本地消息缓冲区中的指针重新设置到缓冲区的开始位置。这样 在随后调用PACK\_MESSAGE的时候，将覆盖在调用存储过程RESET\_BUFFER前在消息缓冲区中已存在的数据项。

``` {#codeblock_hpz_ubo_hnw}
RESET_BUFFER
```

**示例**

我们把发给John的消息写到本地消息缓冲区中。通过调用存储过程RESET\_BUFFER,这条信息被发 给Bob的消息覆盖了。这条消息是在管道上发送的。

``` {#codeblock_ad1_ufa_2du}
DECLARE
    v_status        INTEGER;
BEGIN
    DBMS_PIPE.PACK_MESSAGE('Hi, John');
    DBMS_PIPE.PACK_MESSAGE('Can you attend a meeting at 3:00, today?');
    DBMS_PIPE.PACK_MESSAGE('If not, is tomorrow at 8:30 ok with you?');
    DBMS_PIPE.RESET_BUFFER;
    DBMS_PIPE.PACK_MESSAGE('Hi, Bob');
    DBMS_PIPE.PACK_MESSAGE('Can you attend a meeting at 9:30, tomorrow?');
    v_status := DBMS_PIPE.SEND_MESSAGE('pipe');
    DBMS_OUTPUT.PUT_LINE('SEND_MESSAGE status: ' || v_status);
END;

SEND_MESSAGE status: 0	
```

在接收到的消息中出现了发给Bob的消息。

``` {#codeblock_kgi_15q_p7s}
DECLARE
    v_item          VARCHAR2(80);
    v_status        INTEGER;
BEGIN
    v_status := DBMS_PIPE.RECEIVE_MESSAGE('pipe',1);
    DBMS_OUTPUT.PUT_LINE('RECEIVE_MESSAGE status: ' || v_status);
    DBMS_PIPE.UNPACK_MESSAGE(v_item);
    DBMS_OUTPUT.PUT_LINE('Item: ' || v_item);
    DBMS_PIPE.UNPACK_MESSAGE(v_item);
    DBMS_OUTPUT.PUT_LINE('Item: ' || v_item);
END;

RECEIVE_MESSAGE status: 0
Item: Hi, Bob
Item: Can you attend a meeting at 9:30, tomorrow?
```

## SEND\_MESSAGE {#section_2xv_26l_75y .section}

函数SEND\_MESSAGE从会话的本地消息缓冲区中将一条消息发送到指定的管道。

``` {#codeblock_hpb_nh3_as6}
status SEND_MESSAGE(pipename VARCHAR2 [, timeout INTEGER ]
  [, maxpipesize INTEGER ])
```

**参数**

|参数名称|描述|
|----|--|
|pipename|管道的名称。|
|timeout|等待时间，以秒为单位。 缺省值是86400000\(表示1000天）。|
|maxpipesize|管道的最大容量，以字节为单位。缺省值是8192字节。|
|Status|操作所返回的状态代码。|

可允许使用的状态代码：

|Status Code|Description|
|-----------|-----------|
|0|Success|
|1|Time out|
|3|Function interrupted|

## UNIQUE\_SESSION\_NAME {#section_3rt_n8x_ayx .section}

函数UNIQUE\_SESSION\_NAME 用于返回当前会话的一个唯一名称。

``` {#codeblock_ady_ee2_pep}
name VARCHAR2 UNIQUE_SESSION_NAME
```

**参数**

|参数名称|描述|
|----|--|
|name|唯一的会话名称。|

**示例**

下面的匿名代码块取出并且显示了一个唯一的会话名称。

``` {#codeblock_yar_g1x_mg4}
DECLARE
    v_session       VARCHAR2(30);
BEGIN
    v_session := DBMS_PIPE.UNIQUE_SESSION_NAME;
    DBMS_OUTPUT.PUT_LINE('Session Name: ' || v_session);
END;

Session Name: PG$PIPE$5$2752
```

## UNPACK\_MESSAGE {#section_t0c_884_86m .section}

存储过程UNPACK\_MESSAGE把本地消息缓冲区中消息的数据项拷贝到程序变量中。在使用 UNPACK\_MESSGAE前，必须使用函数RECEIVE\_MESSAGE把消息放到本地消息缓冲区中。

``` {#codeblock_34y_ui3_mx9}
UNPACK_MESSAGE(item OUT { DATE | NUMBER | VARCHAR2 | RAW })
```

**参数**

|参数名称|描述|
|----|--|
|item|从本地缓冲区中接收数据项的变量，这个变量必须和数据项的类型相兼容。|

## 综合性的示例 {#section_gkh_qbm_dcg .section}

在下面的示例中，我们把一个管道作为一个“邮箱”。使用存储过程创建邮箱，然后在邮箱中增加一 条含有多个数据项的信息（最多有3个数据项）。最后显示在包mailbox中的全部内容。

``` {#codeblock_ip1_znj_1z8}
CREATE OR REPLACE PACKAGE mailbox
IS
    PROCEDURE create_mailbox;
    PROCEDURE add_message (
        p_mailbox   VARCHAR2,
        p_item_1    VARCHAR2,
        p_item_2    VARCHAR2 DEFAULT 'END',
        p_item_3    VARCHAR2 DEFAULT 'END'
    );
    PROCEDURE empty_mailbox (
        p_mailbox   VARCHAR2,
        p_waittime  INTEGER DEFAULT 10
    );
END mailbox;

CREATE OR REPLACE PACKAGE BODY mailbox
IS
    PROCEDURE create_mailbox
    IS
        v_mailbox   VARCHAR2(30);
        v_status    INTEGER;
    BEGIN
        v_mailbox := DBMS_PIPE.UNIQUE_SESSION_NAME;
        v_status := DBMS_PIPE.CREATE_PIPE(v_mailbox,1000,FALSE);
        IF v_status = 0 THEN
            DBMS_OUTPUT.PUT_LINE('Created mailbox: ' || v_mailbox);
        ELSE
            DBMS_OUTPUT.PUT_LINE('CREATE_PIPE failed - status: ' ||
                v_status);
        END IF;
    END create_mailbox;

    PROCEDURE add_message (
        p_mailbox   VARCHAR2,
        p_item_1    VARCHAR2,
        p_item_2    VARCHAR2 DEFAULT 'END',
        p_item_3    VARCHAR2 DEFAULT 'END'
    )
    IS
        v_item_cnt  INTEGER := 0;
        v_status    INTEGER;
    BEGIN
        DBMS_PIPE.PACK_MESSAGE(p_item_1);
        v_item_cnt := 1;
        IF p_item_2 != 'END' THEN
            DBMS_PIPE.PACK_MESSAGE(p_item_2);
            v_item_cnt := v_item_cnt + 1;
        END IF;
        IF p_item_3 != 'END' THEN
            DBMS_PIPE.PACK_MESSAGE(p_item_3);
            v_item_cnt := v_item_cnt + 1;
        END IF;
        v_status := DBMS_PIPE.SEND_MESSAGE(p_mailbox);
        IF v_status = 0 THEN
            DBMS_OUTPUT.PUT_LINE('Added message with ' || v_item_cnt ||
                ' item(s) to mailbox ' || p_mailbox);
        ELSE
            DBMS_OUTPUT.PUT_LINE('SEND_MESSAGE in add_message failed - ' ||
                'status: ' || v_status);
        END IF;
    END add_message;

    PROCEDURE empty_mailbox (
        p_mailbox   VARCHAR2,
        p_waittime  INTEGER DEFAULT 10
    )
    IS
        v_msgno     INTEGER DEFAULT 0;
        v_itemno    INTEGER DEFAULT 0;
        v_item      VARCHAR2(100);
        v_status    INTEGER;
    BEGIN
        v_status := DBMS_PIPE.RECEIVE_MESSAGE(p_mailbox,p_waittime);
        WHILE v_status = 0 LOOP
            v_msgno := v_msgno + 1;
            DBMS_OUTPUT.PUT_LINE('****** Start message #' || v_msgno ||
                ' ******');
            BEGIN
                LOOP
                    v_status := DBMS_PIPE.NEXT_ITEM_TYPE;
                    EXIT WHEN v_status = 0;
                    DBMS_PIPE.UNPACK_MESSAGE(v_item);
                    v_itemno := v_itemno + 1;
                    DBMS_OUTPUT.PUT_LINE('Item #' || v_itemno || ': ' ||
                        v_item);
                END LOOP;
                DBMS_OUTPUT.PUT_LINE('******* End message #' || v_msgno ||
                    ' *******');
                DBMS_OUTPUT.PUT_LINE('*');
                v_itemno := 0;
                v_status := DBMS_PIPE.RECEIVE_MESSAGE(p_mailbox,1);
            END;
        END LOOP;
        DBMS_OUTPUT.PUT_LINE('Number of messages received: ' || v_msgno);
        v_status := DBMS_PIPE.REMOVE_PIPE(p_mailbox);
        IF v_status = 0 THEN
            DBMS_OUTPUT.PUT_LINE('Deleted mailbox ' || p_mailbox);
        ELSE
            DBMS_OUTPUT.PUT_LINE('Could not delete mailbox - status: '
                || v_status);
        END IF;
    END empty_mailbox;
END mailbox;
```

下面演示了在包mailbox中执行存储过程的情况。第一个存储过程创建了一个公有管道，这个管道 的名称是由函数UNIQUE\_SESSION\_NAME 产生。

``` {#codeblock_uah_l4a_trv}
EXEC mailbox.create_mailbox;

Created mailbox: PG$PIPE$13$3940
```

通过使用邮箱名称，在同一数据库中，任何访问包mailbox和DBMS\_PIPE的用户都能够添加消息。

``` {#codeblock_e4k_q5p_s5z}
EXEC mailbox.add_message('PG$PIPE$13$3940','Hi, John','Can you attend a meeting at 3:00, today?','-- Mary');

Added message with 3 item(s) to mailbox PG$PIPE$13$3940

EXEC mailbox.add_message('PG$PIPE$13$3940','Don''t forget to submit your report','Thanks,','-- Joe');

Added message with 3 item(s) to mailbox PG$PIPE$13$3940
```

最后，清空包mailbox中的内容：

``` {#codeblock_02h_sa6_5sl}
EXEC mailbox.empty_mailbox('PG$PIPE$13$3940');

****** Start message #1 ******
Item #1: Hi, John
Item #2: Can you attend a meeting at 3:00, today?
Item #3: -- Mary
******* End message #1 *******
*
****** Start message #2 ******
Item #1: Don't forget to submit your report
Item #2: Thanks,
Item #3: Joe
******* End message #2 *******
*
Number of messages received: 2
Deleted mailbox PG$PIPE$13$3940
```

