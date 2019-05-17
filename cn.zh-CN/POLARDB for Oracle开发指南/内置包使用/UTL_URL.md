# UTL\_URL {#concept_221993 .concept}

包UTL\_URL提供转换URL中的非法字符和保留字符的方法。

|Function/Procedure|Return Type|Description|
|------------------|-----------|-----------|
|ESCAPE\(url, escape reserved chars, url\_charset\)|VARCHAR2|Use the ESCAPE function to escape any illegal and reserved characters in a URL.|
|UNESCAPE\(url, url charset\)|VARCHAR2|The UNESCAPE function to convert an URL to it's original form.|

如果对一个函数的调用包含了格式不正确的URL，那么包UTL\_URL将返回异常BAD\_URL。

## ESCAPE {#section_4sy_anw_zgi .section}

使用函数ESCAPE来转换URL中的非法字符和保留字符。语法如下：

``` {#codeblock_zhd_lne_wfc}
ESCAPE(url VARCHAR2, escape_reserved_chars BOOLEAN, url_charset VARCHAR2)
```

保留字符将由一个百分号代替，且后面有两位给转换字符的ascii 值的十六进制代码。

**参数**

|参数名称|描述|
|----|--|
|url|url 用于指定UTL\_URL 将要转换的统一资源定位符。|
|escape reserved chars|escape\_reserved\_chars 是一个BOOLEAN 值，用于命令函数ESCAPE 来转换保留字符和非法字符。 -   如果 escaped\_reserved\_chars 为 FALSE, 那么函数ESCAPE 将只转换指定URL 中的非法字符。
-   如果 escape\_reserved\_chars 为 TRUE, 那么函数ESCAPE 将转换指定URL 中的非法字符和保留字符。通过缺省，escape\_reserved\_chars 为FALSE。

 在 URL中，合法字符参见[表 2](#table_4fv_glu_1pl)。

 在URL的某些部分中，一些字符为合法字符，但在其它部分中却为非法字符。可参考RFC 2396来回顾关于非法字符的综合性条例。一些字符示例在URL的任何部分中都是非法字符，请参见[表 3](#table_own_8kc_1pp)。

 函数 ESCAPE 将保留下列字符（请参见[表 4](#table_1na_u27_vbw)），且如果把escape\_reserved\_chars 设为TRUE 的话，函数ESCAPE 将对保留下来的字符进行转换。

 |
|url\_charset|url\_charset 用于在转换指定字符前，来指定字符将要转换到的字符集。如果url\_charset 为NULL ，那么字符将不会被转换。 url\_charset 的缺省值为ISO-8859-1。|

|Uppercase A through Z|Lowercase a through z|0 through 9|
|asterisk \(\*\)|exclamation point \(!\)|hyphen \(-\)|
|left parenthesis \(\(\)|period \(.\)|right parenthesis \(\)\)|
|single-quote \('\)|tilde \(~\)|underscore \(\_\)|

|Illegal Character|Escape Sequence|
|-----------------|---------------|
|a blank space \( \)|%20|
|curly braces \(\{ or \}\)|%7b and %7d|
|hash mark \(\#\)|%23|

|Reserved Character|Escape Sequence|
|------------------|---------------|
|ampersand \(&\)|%5C|
|at sign \(@\)|%25|
|colon \(:\)|%3a|
|comma \(,\)|%2c|
|dollar sign \($\)|%24|
|equal sign \(=\)|%3d|
|plus sign \(+\)|%2b|
|question mark \(?\)|%3f|
|semi-colon \(;\)|%3b|
|slash \(/\)|%2f|

**示例**

下列匿名代码块使用了函数ESCAPE 来转换URL 中的空白处：

``` {#codeblock_7xa_e64_j2c}
DECLARE
  result varchar2(400);
BEGIN
 result := UTL_URL.ESCAPE('http://www.example.com/Using the ESCAPE function.html');
  DBMS_OUTPUT.PUT_LINE(result);
END;
```

转换后的 URL 为：

``` {#codeblock_cnf_xkq_fk5}
http://www.example.com/Using%20the%20ESCAPE%20function.html
```

当调用函数ESCAPE时，如果我们给escape\_reserved\_chars参数包括一个TRUE值：

``` {#codeblock_f71_3m6_nri}
DECLARE
  result varchar2(400);
BEGIN
 result := UTL_URL.ESCAPE('http://www.example.com/Using the ESCAPE function.html', TRUE);
  DBMS_OUTPUT.PUT_LINE(result);
END;
```

那么函数ESCAPE将转换URL中的保留字符和非法字符：

``` {#codeblock_wp7_s5s_6eh}
http%3A%2F%2Fwww.example.com%2FUsing%20the%20ESCAPE%20function.html
```

## UNESCAPE {#section_ls1_r3w_zn1 .section}

函数UNESCAPE用于删除由函数ESCAPE添加到URL中的转换字符，将URL转换为它的初始格式。语法如下：

``` {#codeblock_xql_qyr_och}
UNESCAPE(url VARCHAR2, url_charset VARCHAR2)
```

**参数**

|参数名称|描述|
|----|--|
|url|url 用于指定UTL\_URL 将要转回的统一资源定位符。|
|url\_charset|在转回一个字符之后，这个字符将假定为url\_charset编码。且在返回之前，将从url\_charset编码转换到数据库编码。如果url\_charset为NULL，那么字符将不被转换。url charset的缺省值为ISO-8 85 9-1。|

**示例**

下列匿名代码块使用了函数ESCAPE来转换URL中的空白处：

``` {#codeblock_x55_r7m_vmi}
DECLARE
  result varchar2(400);
BEGIN
 result := UTL_URL.UNESCAPE('http://www.example.com/Using%20the%20UNESCAPE%20function.html');
  DBMS_OUTPUT.PUT_LINE(result);
END;
```

转换后的URL为：

``` {#codeblock_1cx_xmg_0o8}
http://www.example.com/Using the UNESCAPE function.html
```

