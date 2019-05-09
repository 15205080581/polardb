# DBMS\_CRYPTO {#concept_221978 .concept}

DBMS\_CRYPTO包提供的函数和存储过程允许我们对RAW、BLOB 或 CLOB数据进行加密或解密。我们可以使用DBMS\_CRYPTO函数来产生加密型强随机值。

|Function/Procedure|Return Type|Description|
|------------------|-----------|-----------|
|DECRYPT\(src, typ, key, iv\)|RAW|Decrypts RAW data.|
|DECRYPT\(dst INOUT, src, typ, key, iv\)|N/A|Decrypts BLOB data.|
|DECRYPT\(dst INOUT, src, typ, key, iv\)|N/A|Decrypts CLOB data.|
|ENCRYPT\(src, typ, key, iv\)|RAW|Encrypts RAW data.|
|ENCRYPT\(dst INOUT, src, typ, key, iv\)|N/A|Encrypts BLOB data.|
|ENCRYPT\(dst INOUT, src, typ, key, iv\)|N/A|Encrypts CLOB data.|
|HASH\(src, typ\)|RAW|Applies a hash algorithm to RAW data.|
|HASH\(src\)|RAW|Applies a hash algorithm to CLOB data.|
|MAC\(src, typ, key\)|RAW|Returns the hashed MAC value of the given RAW data using the specified hash algorithm and key.|
|MAC\(src, typ, key\)|RAW|Returns the hashed MAC value of the given CLOB data using the specified hash algorithm and key.|
|RANDOMBYTES\(number bytes\)|RAW|Returns a specified number of cryptographically strong random bytes.|
|RANDOMINTEGER\(\)|INTEGER|Returns a random INTEGER.|
|RANDOMNUMBER\(\)|NUMBER|Returns a random NUMBER.|

DBMS\_CRYPTO函数和存储过程支持下列与Oracle兼容的错误消息：

``` {#codeblock_03m_b2e_5kg}
ORA-28239 - DBMS_CRYPTO.KeyNull
ORA-28829 - DBMS_CRYPTO.CipherSuiteNull
ORA-28827 - DBMS_CRYPTO.CipherSuiteInvalid
```

与Oracle不同的是，如果我们对之前加密的信息再加密，Advanced Server将不会返回错误ORA-28233。

需要注意的是，RAW和BLOB是PostgreSQL BYTEA数据类型的同义词，CLOB是TEXT的同义词。

## DECRYPT {#section_66i_m8o_n77 .section}

通过使用用户指定的加密算法、键及可选的初始化向量，函数DECRYPT或存储过程DECRYPT可解密数据。函数DECRYPT的语法如下：

``` {#codeblock_n9i_d8n_g6a}
DECRYPT
  (src IN RAW, typ IN INTEGER, key IN RAW, iv IN RAW 
   DEFAULT NULL) RETURN RAW
			
```

存储过程DECRYPT的语法如下：

``` {#codeblock_q9m_lfq_yrn}
DECRYPT
  (dst INOUT BLOB, src IN BLOB, typ IN INTEGER, key IN RAW, 
   iv IN RAW DEFAULT NULL)
```

或

``` {#codeblock_oqm_510_trl}
DECRYPT
  (dst INOUT CLOB, src IN CLOB, typ IN INTEGER, key IN RAW, 
   iv IN RAW DEFAULT NULL) 
```

当把DECRYPT作为存储过程调用时，DECRYPT返回给用户指定的BLOB的是BLOB或CLOB数据。

**参数**

 `dst` 

Dst用于指定BLOB数据的名称，存储过程DECRYPT的输出将会编写到这个指定名称的BLOB数据中。存储过程DECRYPT将覆写当前dst中任何已有的数据。

 `src` 

Src用于指定要解密的源数据。如果我们把DECRYPT作为函数调用，那么就要指定RAW数据。如果我们把DECRYPT作为存储过程调用，那么就要指定BLOB或CLOB数据。

 `typ` 

typ用于指定分组密码类型及任何修改器。 当对src加密时，应和指定的类型相匹配。Advanced Server支持下列表中的分组加密算法、修改器及密码组：

|**Block Cipher Algorithms**|
|ENCRYPT\_DES|CONSTANT INTEGER := 1;|
|ENCRYPT\_3DES|CONSTANT INTEGER := 3;|
|ENCRYPT\_AES|CONSTANT INTEGER := 4;|
|ENCRYPT\_AES128|CONSTANT INTEGER := 6;|
|**Block Cipher Modifiers**|
|CHAIN\_CBC|CONSTANT INTEGER := 256;|
|CHAIN\_ECB|CONSTANT INTEGER := 768;|
|**Block Cipher Padding Modifiers**|
|PAD\_PKCS5|CONSTANT INTEGER := 4096;|
|PAD\_NONE|CONSTANT INTEGER := 8192;|
|**Block Cipher Suites**|
|DES\_CBC\_PKCS5|CONSTANT INTEGER := ENCRYPT\_DES + CHAIN\_CBC + PAD\_PKCS5;|
|DES3\_CBC\_PKCS5|CONSTANT INTEGER := ENCRYPT\_3DES + CHAIN\_CBC + PAD\_PKCS5;|
|AES\_CBC\_PKCS5|CONSTANT INTEGER := ENCRYPT\_AES + CHAIN\_CBC + PAD\_PKCS5;|

 `key` 

Key用于指定用户定义的解密键。当对src加密时，应和指定的键相匹配。

 `iv` 

i v \(可选的\)用于指定初始化向量。当对src加密时，如果指定了一个初始化向量，那么我们必须在解密src时也指定一个初始化向量。缺省值为NULL：

**示例**

下列示例使用函数DBMS\_CRYPTO .DECRYPT来解密从表passwords中检索出的加密的口令。

``` {#codeblock_9de_4xe_wba}
CREATE TABLE passwords
(
  principal  VARCHAR2(90) PRIMARY KEY,  -- username
  ciphertext RAW(9)                     -- encrypted password
);
CREATE FUNCTION get_password(username VARCHAR2) RETURN RAW AS
 typ        INTEGER := DBMS_CRYPTO.DES_CBC_PKCS5;
 key        RAW(128) := 'my secret key';
 iv         RAW(100) := 'my initialization vector';
 password   RAW(2048);
BEGIN

  SELECT ciphertext INTO password FROM passwords WHERE principal = username;

  RETURN dbms_crypto.decrypt(password, typ, key, iv);
END;
```

需要注意的是，当调用DECRYPT时，我们必须传递在ENCRYPTING对象时使用过的相同的密码类型、键值及初始化向量。

## ENCRYPT {#section_onh_0v5_8ti .section}

函数ENCRYPT或存储过程ENCRYPT使用用户定义的算法、键及可选的初始化向量来对RAW、BLOB 或 CLOB数据加密。函数ENCRYPT的语法如下：

``` {#codeblock_0cn_5ij_phg}
ENCRYPT
  (src IN RAW, typ IN INTEGER, key IN RAW, 
   iv IN RAW DEFAULT NULL) RETURN RAW
```

存储过程ENCRYPT的语法如下：

``` {#codeblock_xd6_cdq_1ez}
ENCRYPT
  (dst INOUT BLOB, src IN BLOB, typ IN INTEGER, key IN RAW, 
   iv IN RAW DEFAULT NULL)
```

或

``` {#codeblock_476_h0r_57y}
ENCRYPT
  (dst INOUT BLOB, src IN CLOB, typ IN INTEGER, key IN RAW, 
   iv IN RAW DEFAULT NULL) 
```

当把ENCRYPT作为存储过程调用时，ENCRYPT返回给用户指定的BLOB的是BLOB或CLOB数据。

**参数**

 `dst` 

Dst用于指定BLOB数据的名称，存储过程ENCRYPT的输出将会编写到这个指定名称的BLOB数据中。存储过程ENCRYPT将覆写当前dst中任何已有的数据。

 `src` 

Src用于指定要加密的源数据。如果我们把ENCRYPT作为函数调用，那么就要指定RAW数据。如果我们把ENCRYPT 作为存储过程调用，那么就要指定BLOB或CLOB数据。

 `typ` 

typ用于指定由ENCRYPT和任何修改器将要使用的分组密码类型及任何修改器。Advanced Server支持下列表中的分组加密算法、修改器及密码组：

|**Block Cipher Algorithms**|
|ENCRYPT\_DES|CONSTANT INTEGER := 1;|
|ENCRYPT\_3DES|CONSTANT INTEGER := 3;|
|ENCRYPT\_AES|CONSTANT INTEGER := 4;|
|ENCRYPT\_AES128|CONSTANT INTEGER := 6;|
|**Block Cipher Modifiers**|
|CHAIN\_CBC|CONSTANT INTEGER := 256;|
|CHAIN\_ECB|CONSTANT INTEGER := 768;|
|**Block Cipher Padding Modifiers**|
|PAD\_PKCS5|CONSTANT INTEGER := 4096;|
|PAD\_NONE|CONSTANT INTEGER := 8192;|
|**Block Cipher Suites**|
|DES\_CBC\_PKCS5|CONSTANT INTEGER := ENCRYPT\_DES + CHAIN\_CBC + PAD\_PKCS5;|
|DES3\_CBC\_PKCS5|CONSTANT INTEGER := ENCRYPT\_3DES + CHAIN\_CBC + PAD\_PKCS5;|
|AES\_CBC\_PKCS5|CONSTANT INTEGER := ENCRYPT\_AES + CHAIN\_CBC + PAD\_PKCS5;|

 `key` 

Key用于指定加密键。

 `iv` 

i v \(可选的\)用于指定初始化向量。通过缺省方式，iv值为NULL。

**示例**

下列示例使用了DBMS\_CRYPTO.DES\_CBC\_PKCS5分组密码组（一组预先定义的算法和修改器）来对从表passwords中检索出的值加密：

``` {#codeblock_1mg_rh1_t70}
CREATE TABLE passwords
(
  principal  VARCHAR2(90) PRIMARY KEY,  -- username
  ciphertext RAW(9)                     -- encrypted password
);
CREATE PROCEDURE set_password(username VARCHAR2, cleartext RAW) AS
 typ        INTEGER := DBMS_CRYPTO.DES_CBC_PKCS5;
 key        RAW(128) := 'my secret key';
 iv         RAW(100) := 'my initialization vector';
 encrypted  RAW(2048);
BEGIN
  encrypted := dbms_crypto.encrypt(cleartext, typ, key, iv); 
  UPDATE passwords SET ciphertext = encrypted WHERE principal = username;
END;
```

当对password 加密时，ENCRYPT使用了my secret key的一个键值和my initialization vector的一个初始化向量。那么当解密password时就要指定相同的键和初始化向量。

## HASH {#section_0wc_ja5_wfl .section}

函数HASH使用了一个用户指定的算法来返回RAW或CLOB值的哈希值。有三种可使用的HASH函数形式：

``` {#codeblock_s0p_g4n_hv4}
HASH
  (src IN RAW, typ IN INTEGER) RETURN RAW
HASH
  (src IN CLOB, typ IN INTEGER) RETURN RAW 
```

**参数**

 `src` 

src 用于指定将要产生的哈希值。我们可以指定一个RAW、 BLOB或 CLOB值。

 `typ` 

typ 用于指定HASH 函数类型。 Advanced Server支持下列HASH函数类型。

|HASH Functions|
|--------------|
|HASH\_MD4|CONSTANT INTEGER := 1;|
|HASH\_MD5|CONSTANT INTEGER := 2;|
|HASH\_SH1|CONSTANT INTEGER := 3;|

**示例**

下列示例使用了DBMS\_CRYPTO.HASH来查找字符串cleartext source的md5哈希值：

``` {#codeblock_e3y_1jp_u7c}
DECLARE
  typ        INTEGER := DBMS_CRYPTO.HASH_MD5;
  hash_value RAW(100);
BEGIN

  hash_value := DBMS_CRYPTO.HASH('cleartext source', typ);

END;
```

## MAC {#section_yo6_0nj_0ij .section}

MAC 函数使用了一个用户指定的MAC 函数来返回RAW 或CLOB 值的MAC 哈希值。MAC 函数有三种形式：

``` {#codeblock_y57_870_aog}
MAC
  (src IN RAW, typ IN INTEGER, key IN RAW) RETURN RAW
MAC
  (src IN CLOB, typ IN INTEGER, key IN RAW) RETURN RAW
```

**参数**

 `src` 

src 用于指定将要产生的MAC值。我们可以指定一个RAW、 BLOB或 CLOB值。

 `typ` 

typ 用于指定要使用的MAC函数。 Advanced Server支持下列MAC 函数：

|MAC Functions|
|-------------|
|HMAC MD5|CONSTANT INTEGER := 1;|
|HMAC SH1|CONSTANT INTEGER := 2;|

 `key` 

key 用于指定将要用来计算MAC 哈希值的键。

**示例**

下面为查找字符串cleartext source 的MAC 哈希值的示例：

``` {#codeblock_til_jup_n7a}
DECLARE
  typ       INTEGER := DBMS_CRYPTO.HMAC_MD5;
  key       RAW(100) := 'my secret key';
  mac_value RAW(100);
BEGIN

  mac_value := DBMS_CRYPTO.MAC('cleartext source', typ, key);

END;
```

在计算cleartext source的MAC值时，DBMS\_CRYPTO.MAC使用了my secret key的键值。

## RANDOMBYTES {#section_ce2_59c_tde .section}

RANDOMBYTES函数返回的是指定长度的RAW值，包含加密的随机字节。语法如下：

``` {#codeblock_lo9_mmg_pkl}
RANDOMBYTES
  (number_bytes IN INTEGER) RETURNS RAW
```

**参数**

 `number bytes` 

number\_bytes 用于指定要返回的随机字节的数量。

**示例**

下列示例使用RANDOMBYTES 返回的值长度为102 4 字节：

``` {#codeblock_ny3_dzg_18c}
DECLARE
  result RAW(1024);
BEGIN
  result := DBMS_CRYPTO.RANDOMBYTES(1024);
END;
```

## RANDOMINTEGER {#section_c3y_3o2_be2 .section}

RANDOMINTEGER\(\) 函数返回的是一个介于0 和 2 68, 435, 455之间的随机INTEGER。语法如下：

``` {#codeblock_uh2_xe4_k9c}
RANDOMINTEGER() RETURNS INTEGER
```

**示例**

下列示例使用了RANDOMINTEGER函数来返回加密型随机INTEGER值：

``` {#codeblock_am2_07y_dbh}
DECLARE
  result INTEGER;
BEGIN
  result := DBMS_CRYPTO.RANDOMINTEGER();
  DBMS_OUTPUT.PUT_LINE(result);
END;
```

## RANDOMNUMBER {#section_xns_7k3_yv8 .section}

RANDOMNUMBER\(\)函数返回的随机NUMBER介于0 和2 68, 435, 455之间。语法如下：

``` {#codeblock_6js_j8i_26p}
RANDOMNUMBER() RETURNS NUMBER
```

**示例**

下列示例使用了RANDOMINTEGER函数来返回加密型随机数字：

``` {#codeblock_9o5_pq9_v7b}
DECLARE
  result NUMBER;
BEGIN
  result := DBMS_CRYPTO.RANDOMNUMBER();
  DBMS_OUTPUT.PUT_LINE(result);
END;
```

