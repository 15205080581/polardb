# UTL\_ENCODE {#concept_221991 .concept}

UTL\_ENCODE 包提供编码数据及解码数据的方法。

|Function/Procedure|Return Type|Description|
|------------------|-----------|-----------|
|BASE64\_DECODE\(r\)|RAW|Use the BASE64\_DECODE function to translate a Base64 encoded string to the original RAW value.|
|BASE64\_ENCODE\(r\)|RAW|Use the BASE64\_ENCODE function to translate a RAW string to an encoded Base64 value.|
|BASE64\_ENCODE\(loid\)|TEXT|Use the BASE64\_ENCODE function to translate a TEXT string to an encoded Base64 value.|
|MIMEHEADER\_DECODE\(buf\)|VARCHAR2|Use the MIMEHEADER\_DECODE function to translate an encoded MIMEHEADER formatted string to it's original value.|
|MIMEHEADER\_ENCODE\(buf, encode\_charset, encoding\)|VARCHAR2|Use the MIMEHEADER\_ENCODE function to convert and encode a string in MIMEHEADER format.|
|QUOTED\_PRINTABLE\_DECODE\(r\)|RAW|Use the QUOTED\_PRINTABLE\_DECODE function to translate an encoded string to a RAW value.|
|QUOTED\_PRINTABLE\_ENCODE\(r\)|RAW|Use the QUOTED\_PRINTABLE\_ENCODE function to translate an input string to a quoted-printable formatted RAW value.|
|TEXT\_DECODE\(buf, encode\_charset, encoding\)|VARCHAR2|Use the TEXT\_DECODE function to decode a string encoded by TEXT\_ENCODE.|
|TEXT\_ENCODE\(buf, encode\_charset, encoding\)|VARCHAR2|Use the TEXT\_ENCODE function to translate a string to a user-specified character set, and then encode the string.|
|UUDECODE\(r\)|RAW|Use the UUDECODE function to translate a uuencode encoded string to a RAW value.|
|UUENCODE\(r, type, filename, permission\)|RAW|Use the UUENCODE function to translate a RAW string to an encoded uuencode value.|

## BASE64 DECODE {#section_85p_00s_o9l .section}

使用BASE64\_DECODE函数将Base64编码的字符串转换为最初由BASE64\_ENCODE编码的初始值。语法如下：

``` {#codeblock_q5o_uq5_cos}
BASE64_DECODE(r IN RAW)
```

这个函数返回的是一个RAW 值。

**参数**

|参数名称|描述|
|----|--|
|r|r 是一个包含Base64 编码的数据字符串，且这个Base64 编码的数据将被转换为RAW 形式。|

**示例**

**说明：** 在执行下列示例之前，要调用命令：

``` {#codeblock_sqs_52t_zni}
SET bytea_output = escape;
```

这个指令用于命令服务器忽略任何非输出字符，且用可读形式在屏幕上显示BYTEA或RAW值。更多信息，请参考Postgres核心文件，网址如下：[http://www.enterprisedb.com/docs/en/9.3/pg/datatype-binary.html](http://www.enterprisedb.com/docs/en/9.3/pg/datatype-binary.html)

下列示例先编码（使用BASE64\_ENCODE）一个包含文本abc的字符串，再对这个字符串进行解码（使用BASE64\_ENCODE）：

``` {#codeblock_66g_muh_pxq}
edb=# SELECT UTL_ENCODE.BASE64_ENCODE(CAST ('abc' AS RAW));
 base64_encode
---------------
 YWJj
(1 row)

edb=# SELECT UTL_ENCODE.BASE64_DECODE(CAST ('YWJj' AS RAW));
 base64_decode
---------------
 abc
(1 row)
```

## BASE64\_ENCODE {#section_joh_hkw_gav .section}

使用BASE64\_ENCODE函数转换及编码Base64格式的字符串（如在RFC 4648中描述）。在我们打算使用UTL\_SMTP包发送邮件的情况下，BASE64\_ENCODE函数在撰写MIME邮件时非常有用。BASE64\_ENCODE函数有两种语法：

``` {#codeblock_7ma_ip5_4w9}
BASE64_ENCODE(r IN RAW)
```

和

``` {#codeblock_58f_3o0_7ki}
BASE64_ENCODE(loid IN OID)
```

这个函数返回的是一个RAW值或OID。

**参数**

|参数名称|描述|
|----|--|
|r|r 用于指定将被转换为Base64格式的RAW 字符串。|
|loid|loid 用于指定将被转换为Base64格式的大对象的对象ID。|

**示例**

**说明：** 在执行下列示例之前，要调用命令：

``` {#codeblock_pqp_g2s_jde}
SET bytea_output = escape;
```

这个指令用于命令服务器忽略任何非输出字符，且用可读形式在屏幕上显示BYTEA或RAW值。更多信息，请参考Postgres核心文件，网址如下：[http://www.enterprisedb.com/docs/en/9.3/pg/datatype-binary.html](http://www.enterprisedb.com/docs/en/9.3/pg/datatype-binary.html)

下列示例先编码（使用BASE64\_ENCODE）一个包含文本abc的字符串，再对这个字符串进行解码（使用BASE64\_ENCODE）：

``` {#codeblock_h5r_2mp_pt5}
edb=# SELECT UTL_ENCODE.BASE64_ENCODE(CAST ('abc' AS RAW));
 base64_encode
---------------
 YWJj
(1 row)

edb=# SELECT UTL_ENCODE.BASE64_DECODE(CAST ('YWJj' AS RAW));
 base64_decode
---------------
 abc
(1 row)
```

## MIMEHEADER\_DECODE {#section_1n6_ypi_bih .section}

使用MIMEHEADER\_DECODE函数解码由MIMEHEADER\_ENCODE函数编码的值。语法如下：

``` {#codeblock_4qz_75h_rh5}
MIMEHEADER_DECODE(buf IN VARCHAR2)
```

这个函数返回的是一个VARCHAR2 值。

**参数**

|参数名称|描述|
|----|--|
|buf|buf 包含要被解码的值 \(由MIMEHEADER\_ENCODE函数编码\) 。|

**示例**

下列示例先使用MIMEHEADER\_ENCODE函数编码一个字符串，然后再使用MIMEHEADER\_DECODE函数解码这个字符串：

``` {#codeblock_w3b_5sq_ymh}
edb=# SELECT UTL_ENCODE.MIMEHEADER_ENCODE('What is the date?') FROM DUAL;
      mimeheader_encode
------------------------------
 =?UTF8?Q?What is the date??=
(1 row)

edb=# SELECT UTL_ENCODE.MIMEHEADER_DECODE('=?UTF8?Q?What is the date??=') FROM DUAL;
 mimeheader_decode
-------------------
 What is the date?
(1 row)
```

## MIMEHEADER\_ENCODE {#section_8li_hwy_842 .section}

先使用MIMEHEADER\_ENCODE函数将字符串转换为mime标头格式，再对这个字符串编码。语法如下：

``` {#codeblock_88d_uim_31z}
MIMEHEADER_ENCODE(buf IN VARCHAR2, encode_charset IN VARCHAR2 DEFAULT NULL, encoding IN INTEGER DEFAULT NULL)
```

这个函数返回的是一个VARCHAR2 值。

**参数**

|参数名称|描述|
|----|--|
|buf|buf 包含要被格式化和编码的字符串。这个字符串是一个VARCHAR2值。|
|encode charset|encode\_charset 用于在格式化和编码字符串之前，指定字符串将要转换为的字符集。缺省值为NULL。|
|encoding|encoding 用于指定在编码字符串时使用的编码类型。我们可以指定以下两种编码类型： -   指定Q编码类型来启用quoted-printable 编码。如果我们没有指定一个值，那么MIMEHEADER\_ENCODE 将使用quoted-printable 编码。
-   指定B 来启用base-64 编码。

 |

**示例**

下列示例先使用MIMEHEADER\_ENCODE函数编码一个字符串，然后再使用MIMEHEADER\_DECODE函数解码这个字符串：

``` {#codeblock_on1_cs3_qa6}
edb=# SELECT UTL_ENCODE.MIMEHEADER_ENCODE('What is the date?') FROM DUAL;
      mimeheader_encode
------------------------------
 =?UTF8?Q?What is the date??=
(1 row)

edb=# SELECT UTL_ENCODE.MIMEHEADER_DECODE('=?UTF8?Q?What is the date??=') FROM DUAL;
 mimeheader_decode
-------------------
 What is the date?
(1 row)
```

## QUOTED\_PRINTABLE\_DECODE {#section_z5x_5jc_t7m .section}

使用 QUOTED\_PRINTABLE\_DECODE 函数将一个编码的quoted-printable 字符串转换为一个解码的RAW 字符串。语法如下：

``` {#codeblock_7rp_75e_l13}
QUOTED_PRINTABLE_DECODE(r IN RAW)
```

这个函数返回的是一个RAW 值。

**参数**

|参数名称|描述|
|----|--|
|r|r 包含将要被解码的编码字符串。这个字符串是一个RAW 值，由QUOTED\_PRINTABLE\_ENCODE 编码。|

**示例**

**说明：** 在执行下列示例之前，先调用命令：

``` {#codeblock_kzr_jq8_xkt}
SET bytea_output = escape;
```

这个指令用于命令服务器忽略任何非输出字符，且用可读形式在屏幕上显示BYTEA或RAW值。更多信息，请参考Postgres核心文件，网址如下：[http://www.enterprisedb.com/docs/en/9.3/pg/datatype-binary.html](http://www.enterprisedb.com/docs/en/9.3/pg/datatype-binary.html)

下列示例先编码一个字符串，再对这个字符串解码：

``` {#codeblock_11y_fx7_hef}
edb=# SELECT UTL_ENCODE.QUOTED_PRINTABLE_ENCODE('E=mc2') FROM DUAL;  quoted_printable_encode
-------------------------
 E=3Dmc2
(1 row)

edb=# SELECT UTL_ENCODE.QUOTED_PRINTABLE_DECODE('E=3Dmc2') FROM DUAL;
 quoted_printable_decode
-------------------------
 E=mc2
(1 row)
```

## QUOTED\_PRINTABLE\_ENCODE {#section_1oz_cwn_x14 .section}

使用 QUOTED\_PRINTABLE\_ENCODE 函数将字符串转换并编码为quoted-printable 格式。语法如下：

``` {#codeblock_znv_79r_br3}
QUOTED_PRINTABLE_ENCODE(r IN RAW)
```

这个函数返回的是一个 RAW 值。

**参数**

|参数名称|描述|
|----|--|
|r|r包含要被编码为quoted-printable 格式的RAW值的字符串。|

**示例**

**说明：** 在执行下列示例之前，先调用命令：

``` {#codeblock_hdu_fuo_vxy}
SET bytea_output = escape;
					
```

这个指令用于命令服务器忽略任何非输出字符，且用可读形式在屏幕上显示BYTEA或RAW值。更多信息，请参考Postgres核心文件，网址如下：[http://www.enterprisedb.com/docs/en/9.3/pg/datatype-binary.html](http://www.enterprisedb.com/docs/en/9.3/pg/datatype-binary.html)

下列示例先编码一个字符串，再对这个字符串解码：

``` {#codeblock_re0_cie_242}
edb=# SELECT UTL_ENCODE.QUOTED_PRINTABLE_ENCODE('E=mc2') FROM DUAL;  quoted_printable_encode
-------------------------
 E=3Dmc2
(1 row)

edb=# SELECT UTL_ENCODE.QUOTED_PRINTABLE_DECODE('E=3Dmc2') FROM DUAL;
 quoted_printable_decode
-------------------------
 E=mc2
(1 row)
```

## TEXT\_DECODE {#section_zfk_hmu_rpu .section}

使用 TEXT\_DECODE 函数转换并解码一个编码的字符串为VARCHAR2值，这个VARCHAR2值最初是由TEXT\_ENCODE函数编码的。语法如下：

``` {#codeblock_euz_a26_9pz}
TEXT_DECODE(buf IN VARCHAR2, encode_charset IN VARCHAR2 DEFAULT NULL, encoding IN PLS_INTEGER DEFAULT NULL)
```

这个函数返回的是一个VARCHAR2 值。

**参数**

|参数名称|描述|
|----|--|
|buf|buf 包含一个编码的字符串，且这个字符串将被转换为由TEXT\_ENCODE 编码的初始值。|
|encode charset|encode\_charset 用于在编码之前指定字符串将要转换为的字符集。缺省值为NULL。|
|encoding|encoding 用于指定由TEXT\_DECODE使用的编码类型。我们可以指定以下两种编码类型： -   UTL\_ENCODE.BASE64用于指定base-64 编码。
-   UTL\_ENCODE.QUOTED\_PRINTABLE 用于指定quoted printable 编码。这种为缺省。

 |

**示例**

下列示例先使用TEXT\_ENCODE函数编码一个字符串，然后再使用TEXT\_DECODE函数解码这个字符串：

``` {#codeblock_4sg_26b_2r6}
edb=# SELECT UTL_ENCODE.TEXT_ENCODE('What is the date?', 'BIG5', UTL_ENCODE.BASE64) FROM DUAL;
       text_encode
--------------------------
 V2hhdCBpcyB0aGUgZGF0ZT8=
(1 row)

edb=# SELECT UTL_ENCODE.TEXT_DECODE('V2hhdCBpcyB0aGUgZGF0ZT8=', 'BIG5', UTL_ENCODE.BASE64) FROM DUAL;
    text_decode
-------------------
 What is the date?
(1 row)
```

## TEXT\_ENCODE {#section_9y3_4nd_1hg .section}

使用TEXT\_ENCODE 函数将字符串转换为一个用户指定的字符集，然后再对字符串进行编码。语法如下：

``` {#codeblock_htd_8hj_3xi}
TEXT_DECODE(buf IN VARCHAR2, encode_charset IN VARCHAR2 DEFAULT NULL, encoding IN PLS_INTEGER DEFAULT NULL)
```

这个函数返回的是一个VARCHAR2 值。

**参数**

|参数名称|描述|
|----|--|
|buf|buf 包含编码的字符串，且这个字符串将被转换为指定的字符集。 然后由TEXT\_ENCODE编码。|
|encode charset|encode\_charset 用于在编码之前指定值将被转换为的字符集。缺省值为NULL 。|
|encoding|encoding 用于指定由TEXT\_ENCODE使用的编码类型。我们可以指定以下两种编码类型： -   UTL\_ENCODE.BASE64用于指定base-64 编码。
-   UTL\_ENCODE.QUOTED\_PRINTABLE用于指定quoted printable 编码。这种为缺省。

 |

**示例**

下列示例先使用TEXT\_ENCODE函数编码一个字符串，然后再使用TEXT\_DECODE函数解码这个字符串：

``` {#codeblock_g5p_j1t_ilv}
edb=# SELECT UTL_ENCODE.TEXT_ENCODE('What is the date?', 'BIG5', UTL_ENCODE.BASE64) FROM DUAL;
       text_encode
--------------------------
 V2hhdCBpcyB0aGUgZGF0ZT8=
(1 row)

edb=# SELECT UTL_ENCODE.TEXT_DECODE('V2hhdCBpcyB0aGUgZGF0ZT8=', 'BIG5', UTL_ENCODE.BASE64) FROM DUAL;
    text_decode
-------------------
 What is the date?
(1 row)
```

## UUDECODE {#section_of6_e7a_mdw .section}

使用UUDECODE函数将uuencode编码字符串转换并解码为RAW值，这个RAW值最初是由UUENCODE函数编码的。语法如下：

``` {#codeblock_f9y_b6n_lhe}
UUDECODE(r IN RAW)
```

这个函数返回的是一个RAW 值。

**参数**

|参数名称|描述|
|----|--|
|r|r 包含要被转换为RAW 值的uuencoded 字符串。|

**示例**

**说明：** 在执行下列示例之前，要调用命令：

``` {#codeblock_afw_ml3_9x9}
SET bytea_output = escape;
```

这个指令用于命令服务器忽略任何非输出字符，且用可读形式在屏幕上显示BYTEA或RAW值。更多信息，请参考Postgres核心文件，网址如下：[http://www.enterprisedb.com/docs/en/9.3/pg/datatype-binary.html](http://www.enterprisedb.com/docs/en/9.3/pg/datatype-binary.html)

下列示例先使用UUENCODE函数编码一个字符串，然后再使用UUDECODE函数解码这个字符串：

``` {#codeblock_cvf_04c_u26}
edb=# SET bytea_output = escape;
SET
edb=# SELECT UTL_ENCODE.UUENCODE('What is the date?') FROM DUAL;
                              uuencode
--------------------------------------------------------------------
 begin 0 uuencode.txt\01215VAA="!I<R!T:&4@9&%T93\\`\012`\012end\012
(1 row)

edb=# SELECT UTL_ENCODE.UUDECODE
edb-# ('begin 0 uuencode.txt\01215VAA="!I<R!T:&4@9&%T93\\`\012`\012end\012')
edb-# FROM DUAL;
     uudecode
-------------------
 What is the date?
(1 row)
```

## UUENCODE {#section_mhi_brh_hic .section}

使用UUENCODE 函数将RAW 数据转换为uuencode 格式的编码字符串。语法如下：

``` {#codeblock_9v0_adh_chq}
UUENCODE(r IN RAW, type IN INTEGER DEFAULT 1, filename IN VARCHAR2 DEFAULT NULL, permission IN VARCHAR2 DEFAULT NULL)
```

这个函数返回的是一个RAW 值。

**参数**

|参数名称|描述|
|----|--|
|r|r 包含要被转换为uuencode 格式的RAW 字符串。|
|type|type 是一个INTEGER 值或是一个常量。这个常量用于指定要返回的uuencoded 字符串的类型。缺省值为1。可能的值见[表 2](#table_yrx_00l_chl)。|
|filename|filename 是一个 VARCHAR2 值，用于指定我们想要在编码形式中嵌入的文件名称。如果我们不指定文件名称，那么， UUENCODE 将在编码形式中包含uuencode .txt 文件名。|
|permission|permission 是一个VARCHAR2 值，用于指定权限模式。缺省值为NULL。|

|Value|Constant|
|-----|--------|
|1|complete|
|2|header\_piece|
|3|middle\_piece|
|4|end\_piece|

**示例**

**说明：** 在执行下列示例之前，要先调用命令：

``` {#codeblock_fy6_76d_9ye}
SET bytea_output = escape;
```

这个指令用于命令服务器忽略任何非输出字符，且用可读形式在屏幕上显示BYTEA或RAW值。更多信息，请参考Postgres核心文件，网址如下：[http://www.enterprisedb.com/docs/en/9.3/pg/datatype-binary.html](http://www.enterprisedb.com/docs/en/9.3/pg/datatype-binary.html)

下列示例先使用UUENCODE函数编码一个字符串， 然后再使用UUDECODE函数解码这个字符串：

``` {#codeblock_r0u_mts_e3g}
edb=# SET bytea_output = escape;
SET
edb=# SELECT UTL_ENCODE.UUENCODE('What is the date?') FROM DUAL;
                              uuencode
--------------------------------------------------------------------
 begin 0 uuencode.txt\01215VAA="!I<R!T:&4@9&%T93\\`\012`\012end\012
(1 row)

edb=# SELECT UTL_ENCODE.UUDECODE
edb-# ('begin 0 uuencode.txt\01215VAA="!I<R!T:&4@9&%T93\\`\012`\012end\012')
edb-# FROM DUAL;
     uudecode
-------------------
 What is the date?
(1 row)
```

