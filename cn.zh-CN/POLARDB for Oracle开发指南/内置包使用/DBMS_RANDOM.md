# DBMS\_RANDOM {#concept_221985 .concept}

DBMS\_RANDOM包提供了许多方法以产生随机值。下列表中列出了DBMS\_RANDOM包中可使用的存储过程及函数。

|Function/Procedure|Return Type|Description|
|------------------|-----------|-----------|
|INITIALIZE\(val\)|n/a|Initializes the DBMS RANDOM package with the specified seed value. Deprecated, but supported for backward compatibility.|
|NORMAL\(\)|NUMBER|Returns a random NUMBER.|
|RANDOM|INTEGER|Returns a random INTEGER with a value greater than or equal to -2A31 and less than 2A31. Deprecated, but supported for backward compatibility.|
|SEED\(val\)|n/a|Resets the seed with the specified value.|
|SEED\(val\)|n/a|Resets the seed with the specified value.|
|STRING\(opt, len\)|VARCHAR2|Returns a random string.|
|TERMINATE|n/a|TERMINATE has no effect. Deprecated, but supported for backward compatibility.|
|VALUE|NUMBER|Returns a random number with a value greater than or equal to 0 and less than 1, with 38 digit precision.|
|VALUE\(low, high\)|NUMBER|Returns a random number with a value greater than or equal to low and less than high.|

## INITIALIZE {#section_4gw_3cd_lk1 .section}

INITIALIZE存储过程用一个种子值来初始化DBMS\_RANDOM包。语法如下：

``` {#codeblock_ngv_af8_jk4}
INITIALIZE(val IN INTEGER)
```

但一般情况下并不建议使用INITIALIZE存储过程，它仅用于向下兼容。

**参数**

|参数名称|描述|
|----|--|
|val|val 是一个由DBMS\_RANDOM 包算法使用的种子值。|

**示例**

下列代码段演示了对INITIALIZE 存储过程的调用，这个存储过程用种子值64 75对DBMS\_RANDOM包进行初始化。

``` {#codeblock_r0f_wjh_yqz}
DBMS_RANDOM.INITIALIZE(6475);
```

## NORMAL {#section_4tn_oyw_rt3 .section}

NORMAL函数返回的是类型NUMBER的一个随机数。语法如下：

``` {#codeblock_xro_rlf_5e8}
result NUMBER NORMAL()
```

**参数**

|参数名称|描述|
|----|--|
|result|result 是类型NUMBER 的一个随机值。|

**示例**

下列代码段演示了对NORMAL 函数的调用：

``` {#codeblock_tmm_txa_9zw}
x:= DBMS_RANDOM.NORMAL();
```

## RANDOM {#section_f9r_2xt_eh9 .section}

RANDOM函数返回的是一个随机INTEGER值，它大于或等于-2 A31且小于2 A31。语法如下：

``` {#codeblock_ptw_7m2_68f}
result INTEGER RANDOM()
```

但一般情况下并不建议使用RANDOM函数，它仅用于向下兼容。

**参数**

|参数名称|描述|
|----|--|
|result|result 是类型INTEGER的一个随机值。|

**示例**

下列代码段演示了对RANDOM函数的调用。调用后返回的是一个随机数：

``` {#codeblock_s0j_1ar_r1m}
x := DBMS_RANDOM.RANDOM();
```

## SEED {#section_gua_b6v_6s3 .section}

通过SEED存储过程的第二种形式，我们可以用一个字符串值给DBMS\_RANDOM包重置种子值。语法如下：

``` {#codeblock_85a_omd_zbf}
SEED(val IN VARCHAR2)
```

**参数**

|参数名称|描述|
|----|--|
|val|val是由DBMS\_RANDOM 包算法使用的种子值。|

**示例**

下列代码段演示了对SEED存储过程的调用，调用时将种子值设为abc123。

``` {#codeblock_8ic_ggx_m5b}
DBMS_RANDOM.SEED('abc123');
```

## STRING {#section_rs2_2a7_yd7 .section}

STRING函数返回的是一个用户指定形式的随机VARCHAR2字符串。语法如下：

``` {#codeblock_6ei_4sd_j4b}
result VARCHAR2 STRING(opt IN CHAR, len IN NUMBER)
```

**参数**

`Opt`：给返回的字符串的格式化选项。`option`也许为：

|Option|Specifies Formatting Option|
|------|---------------------------|
|u or U|Uppercase alpha string|
|l or L|Lowercase alpha string|
|a or A|Mixed case string|
|x or X|Uppercase alpha-numeric string|
|p or P|Any printable characters|

`len`：返回的字符串长度。

`result`：result 是类型VARCHAR2的一个随机值。

**示例**

下列代码段演示了对STRING函数的调用。调用后返回的是一个随机字母数字式的字符串，长度为10个字符。

``` {#codeblock_0ur_bpl_ebk}
x := DBMS_RANDOM.STRING('X', 10);
```

## TERMINATE {#section_q9o_7r1_g04 .section}

TERMINATE 存储过程不会造成任何影响。语法如下：

``` {#codeblock_uny_ctm_4n0}
TERMINATE
```

但一般情况下并不建议使用TERMINATE存储过程，它仅支持于兼容性。

## VALUE {#section_mz7_xq9_pdc .section}

VALUE函数返回的是一个随机NUMBER，大于或等于0且小于1，数字精度为38。VALUE函数有两种形式，第一种形式的语法为：

``` {#codeblock_lph_7u6_nd3}
result NUMBER VALUE()
```

**参数**

|参数名称|描述|
|----|--|
|result|result 是类型NUMBER 的一个随机值。|

**示例**

下列代码段演示了对VALUE函数的调用。调用后返回的是一个随机NUMBER：

``` {#codeblock_acm_bxn_3jc}
x := DBMS_RANDOM.VALUE();
```

## VALUE {#section_fwt_6xg_o3f .section}

VALUE函数返回的是一个介于用户指定边界之间的随机NUMBER值。VALUE函数有两种形式。第二种形式的语法如下：

``` {#codeblock_ymf_749_o9c}
result NUMBER VALUE(low IN NUMBER, high IN NUMBER)
```

**参数**

|参数名称|描述|
|----|--|
|low|low 用于指定随机值的下边界。这个随机值可能等于low 。|
|high|high 用于指定随机值的上边界。这个随机值将会小于high 。|
|result|result是类型NUMBER 的一个随机值。|

**示例**

下列代码段演示了对VALUE函数的调用。调用后返回的是一个随机NUMBER值，大于或等于1且小于100。

``` {#codeblock_nrp_hvo_fdc}
x := DBMS_RANDOM.VALUE(1, 100);
```

