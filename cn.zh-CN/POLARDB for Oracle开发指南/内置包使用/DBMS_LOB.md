# DBMS\_LOB {#concept_221979 .concept}

包DBMS\_LOB用于在大对象上进行操作。

|Function/Procedure|Function or Procedure|Return Type|Description|
|------------------|---------------------|-----------|-----------|
|APPEND\(dest\_lob IN OUT,src\_lob\)|Procedure|n/a|Appends one large object to another.|
|COMPARE\(lob\_1, lob\_2 \[, amount\[, offset\_1 \[, offset\_2 \]\]\]\)|Function|INTEGER|Compares two large objects.|
|CONVERTOBLOB\(dest\_lob IN OUT,src\_clob, amount, dest\_offsetIN OUT, src\_offset IN OUT,blob\_csid, lang\_context IN OUT,warning OUT\)|Procedure|n/a|Converts character data to binary.|
|CONVERTTOCLOB\(dest\_lob IN OUT,src\_blob, amount, dest\_offsetIN OUT, src\_offset IN OUT,blob\_csid, lang\_context IN OUT,warning OUT\)|Procedure|n/a|Converts binary data to character.|
|COPY\(dest\_lob IN OUT, src\_lob,amount \[, dest\_offset \[,src\_offset \]\]\)|Procedure|n/a|Copies one large object to another.|
|ERASE\(lob\_loc IN OUT, amount IN OUT \[, offset \]\)|Procedure|n/a|Erase a large object.|
|GET\_STORAGE\_LIMIT\(lob\_loc\)|Function|INTEGER|Get the storage limit for large objects.|
|GETLENGTH\(lob\_loc\)|Function|INTEGER|Get the length of the large object.|
|INSTR\(lob\_loc, pattern \[,offset \[, nth \]\]\)|Function|INTEGER|Get the position of the nth occurrence of a pattern in the large object starting atoffset.|
|READ\(lob\_loc, amount IN OUT,offset, buffer OUT\)|Procedure|n/a|Read a large object.|
|SUBSTR\(lob\_loc \[, amount \[,offset \]\]\)|Function|RAW,VARCHAR2|Get part of a large object.|
|TRIM\(lob\_loc IN OUT, newlen\)|Procedure|n/a|Trim a large object to the specified length.|
|WRITE\(lob\_loc IN OUT, amount,offset, buffer\)|Procedure|n/a|Write data to a large object.|
|WRITEAPPEND\(lob\_loc IN OUT,amount, buffer\)|Procedure|n/a|Write data from the buffer to the end of a large object.|

与Oracle 版本的DBMS\_LOB执行相比，POLARDB for Oracle的DBMS\_LOB执行是部分执行。POLARDB for Oracle仅支持上述表中列出的函数和存储过程。

下列表中列出的是可在包中使用的公有变量。

|Public Variables|Data Type|Value|
|----------------|---------|-----|
|compress off|INTEGER|0|
|compress\_on|INTEGER|1|
|deduplicate\_off|INTEGER|0|
|deduplicate\_on|INTEGER|4|
|default\_csid|INTEGER|0|
|default\_lang\_ctx|INTEGER|0|
|encrypt\_off|INTEGER|0|
|encrypt\_on|INTEGER|1|
|file\_readonly|INTEGER|0|
|lobmaxsize|INTEGER|1073741823|
|lob\_readonly|INTEGER|0|
|lob\_readwrite|INTEGER|1|
|no\_warning|INTEGER|0|
|opt\_compress|INTEGER|1|
|opt\_deduplicate|INTEGER|4|
|opt\_encrypt|INTEGER|2|
|warn\_inconvertible\_char|INTEGER|1|

在下面的章节中，如果大对象是BLOB类型，那么它的长度和偏移量是以字节为单位测量的。如果大对象是CLOB类型, 那么长度和偏移量是以字符为单位测量的。

## APPEND {#section_n8b_mou_0ii .section}

存储过程APPEND用于将一个大对象附加在另外一个大对象上。这两个大对象必须属于同一类型。

``` {#codeblock_68k_faw_wto}
APPEND(dest_lob IN OUT { BLOB | CLOB }, src_lob { BLOB | CLOB })
```

**参数**

|参数名称|描述|
|----|--|
|dest lob|目标大对象的位置。它必须和参数src\_lob代表的大对象的数据类型一样。|
|src lob|源大对象的位置。它必须和参数dest\_lob代表的大对象的数据类型一样。|

## COMPARE {#section_sez_lx7_46d .section}

存储过程COMPARE在给定的长度和偏移范围内对两个大对象进行逐字节的精确比较。进行比较操作 的两个大对象必须是相同的数据类型。

``` {#codeblock_33n_iev_95o}
status INTEGER COMPARE(lob_1 { BLOB | CLOB },
  lob_2 { BLOB | CLOB }
  [, amount INTEGER [, offset_1 INTEGER [, offset_2 INTEGER ]]])
```

**参数**

|参数名称|描述|
|----|--|
|lob\_1|在比较操作中第一个大对象的位置，和参数lob\_2代表的大对象的数据类型必须相同。|
|lob\_2|在比较操作中第二个大对象的位置，和参数lob\_1代表的大对象的数据类型必须相同。|
|amount|如果大对象的数据类型是BLOB，那么是对两个大对象各自的总字节数进行比较。如果大对象的数据类型是CLOB, 则是对两个大对象各自总的字符数进行比较。这个参数的缺省值是一个大对象的最大容量。|
|offset 1|在比较操作中，第一个大对象中的起始位置。第一个字节/字符的位置是偏移量1，缺省值是1。|
|offset\_2|在比较操作中，第二个大对象中的起始位置。第一个字节/字符的位置是偏移量1，缺省值是1。|
|status|如果在指定的长度和偏移范围内，两个大对象完全相等，这个参数返回0.如果不相等，则返回非零值。如果参数amount, offset\_1, 或者offset\_2小于0，则返回空值。|

## CONVERTTOBLOB {#section_hn8_gyg_he9 .section}

存储过程CONVERTTOBLOB用于将字符类型数据的大对象转换成二进制类型数据的大对象。

``` {#codeblock_hgv_0hg_2ow}
CONVERTTOBLOB(dest_lob IN OUT BLOB, src_clob CLOB,
  amount INTEGER, dest_offset IN OUT INTEGER,
  src_offset IN OUT INTEGER, blob_csid NUMBER,
  lang_context IN OUT INTEGER, warning OUT INTEGER)
```

**参数**

|参数名称|描述|
|----|--|
|dest lob|表示一个BLOB类型的大对象，我们使用存储过程CONVERTTOBLOB把CLOB类型大对象的字符数据转换成BLOB类型大对象的二进制数据。|
|src clob|表示一个CLOB类型的大对象，我们使用存储过程CONVERTTOBLOB把这个大对象的字符类型数据转换成BLOB类型大对象的二进制数据。|
|amount|表示在参数src\_clob所指定的大对象中要转换的字符数量。|
|dest\_offset IN|BLOB类型的目标大对象中字节的位置，其中写入CLOB类型大对象内容的操作应该从这个位置开始。第一个字节是偏移量1。|
|dest\_offset OUT|在写操作完成后，在BLOB类型大对象中字节的位置。第一个字节为偏移变量1。|
|src offset IN|在转换操作中， CLOB类型大对象开始的位置。第一个字符为偏移量1。|
|src\_offset OUT|在转换操作完成后，CLOB类型大对象中字符的位置。第一个字符是偏移量1。|
|blob csid|在BLOB类型大对象中的字符集ID。|
|langcontext IN|在转换操作中使用的语言环境。通常为这个设置使用缺省值0。|
|langcontext OUT|转换完成后的语言环境。|
|warning|如果转换成功，则返回0，如果遇到不可转换的字符，则返回1。|

## CONVERTTOCLOB {#section_vc1_ny8_sab .section}

存储过程CONVERTTOCLOB用于将二进制数据的大对象转换成字符型数据的大对象。

``` {#codeblock_zt1_r7n_vur}
CONVERTTOCLOB(dest_lob IN OUT CLOB, src_blob BLOB,
  amount INTEGER, dest_offset IN OUT INTEGER,
  src_offset IN OUT INTEGER, blob_csid NUMBER,
  lang_context IN OUT INTEGER, warning OUT INTEGER)
```

**参数**

|参数名称|描述|
|----|--|
|dest lob|CLOB类型大对象的位置，我们将把BLOB类型大对象的二进制类型数据转换成CLOB类型大对象的字符类型数据。|
|src\_blob|BLOB类型大对象的位置，我们将把它的二进制数据转换成目标大对象的字符类型数据。|
|amount|在参数src\_blob指定的大对象中要进行转换的字节数量。|
|dest\_offset IN|在CLOB类型大对象中的位置，写入BLOB类型大对象内容的操作应该从这个位置开始。第一个字符是偏移量1。|
|dest\_offset OUT|在写操作完成后在CLOB类型大对象中字符的位置。第一个字符是偏移量1。|
|src offset IN|在进行转换操作时BLOB类型大对象中字节的开始位置。第一个字节是偏移量1。|
|src\_offset OUT|在转换操作完成后，在BLOB类型大对象中字节的位置。第一个字节是偏移量1。|
|blob csid|CLOB类型大对象的字符集ID。|
|CLOB. langcontext IN|转换操作时使用语言环境。通常对于这个设置，使用缺省值0。|
|langcontext OUT|转换操作完成后的语言环境。|
|warning|如果转换成功，返回0，如果遇到不可转换的字符与，则返回1。|

## COPY {#section_prb_gn7_0o3 .section}

存储过程COPY用于将一个大对象复制为另一个大对象。源和目标大对象必须具有相同的数据类型。

``` {#codeblock_x1v_lz0_oe9}
COPY(dest_lob IN OUT { BLOB | CLOB }, src_lob 
{ BLOB | CLOB },
  amount INTEGER
  [, dest_offset INTEGER [, src_offset INTEGER ]])
```

**参数**

|参数名称|描述|
|----|--|
|dest lob|在大对象复制操作中目标大对象的位置。它和参数src\_lob代表的大对象要具有相同的数据类型。|
|src lob|在大对象复制操作中的源大对象的位置。它和参数dest\_lob代表大对象的数据类型必须一样。|
|amount|在参数src\_lob代表的大对象中拷贝的字节或字符数。|
|dest offset|在目标大对象中的位置，是写入源大对象内容操作时的开始位置。第一个位置是偏移量1. 缺省值是1。|
|src offset|在源大对象中的位置，是将源大对象拷贝到目标大对象操作时的开始位置。第一个位置是偏移量1。缺省值是1。|

## ERASE {#section_fhr_dob_d7w .section}

存储过程ERASE用于清除一个大对象的部分数据。清除一个大对象的部分内容就是分别用0字节过滤器替代BLOB类型大对象的部分内容，用空格替代CLOB类型大对象的部分内容。操作结束后而大对象的实际大小不会改变。

``` {#codeblock_bqr_ry4_6dq}
ERASE(lob_loc IN OUT { BLOB | CLOB }, amount IN OUT INTEGER
  [, offset INTEGER ])
```

**参数**

|参数名称|描述|
|----|--|
|lob loc|要进行清除操作的大对象。|
|amount IN|在大对象中要清除的字节或字符数。|
|amount OUT|实际被清除的字节或字符数量。如果在参数amount指定的字节或字符数被清除前已经达到了大对象的末尾，那么这个值会比输入值小一些。|
|offset|对大对象进行清除操作时开始的位置。第一个字节或字符的位置是1。缺省值是1。|

## GET\_STORAGE\_LIMIT {#section_c67_dme_r57 .section}

函数GET\_STORAGE\_LIMIT返回大对象可允许使用的最大存储空间。

``` {#codeblock_gnf_epl_q3z}
size INTEGER GET_STORAGE_LIMIT(lob_loc BLOB)

size INTEGER GET_STORAGE_LIMIT(lob_loc CLOB)
```

**参数**

|参数名称|描述|
|----|--|
|size|在数据库中一个大对象可允许使用的最大存储空间。|
|lob loc|这个参数只是为了与Oracle兼容而提供，在实际运行中可以忽略。|

## GETLENGTH {#section_jgf_kqs_c6u .section}

函数GETLENGTH返回一个大对象的长度。

``` {#codeblock_2dj_4p4_4js}
amount INTEGER GETLENGTH(lob_loc BLOB)

amount INTEGER GETLENGTH(lob_loc CLOB)
```

**参数**

|参数名称|描述|
|----|--|
|lob loc|大对象的位置，我们使用函数GETLENGTH可以获取这个对象的长度。|
|amount|大对象的长度。对于BLOB类型大对象来说，是以字节为单位，而对于CLOB类型大 对象来说，是以字符为单位的。|

## INSTR {#section_aji_yky_loj .section}

函数INSTR返回在大对象中指定模式第n次出现时的位置。

``` {#codeblock_491_sn0_fdr}
position INTEGER INSTR(lob_loc { BLOB | CLOB },
  pattern { RAW | VARCHAR2 } [, offset INTEGER [, nth INTEGER ]])
```

**参数**

|参数名称|描述|
|----|--|
|lob loc|大对象的位置，我们将使用函数INSTR在这个大对象中搜索指定的模式。|
|pattern|以字节为单位或以字符为单位的模式，用于匹配大对象中的内容。如果lob\_loc代表BLOB类型大对象，那么模式必须是RAW类型。如果lob\_loc代表CLOB类型大对象，那么模式必须是VARCHAR2类型。|
|offset|在参数lob\_loc代表的大对象中搜索模式时的开始位置。第一个字节或字符是位置1.缺省值是1。|
|nth|从由给定的偏移量指定起始位置开始搜索第n次出现指定模式。缺省值是1。|
|position|在大对象中的第n次出现模式的位置，搜索的起始位置是由参数offset指定的。|

## READ {#section_xk8_cwl_4xg .section}

存储过程READ用于从大对象中读取部分内容，然后把这部分内容放到到缓冲区中。

``` {#codeblock_4ax_f94_yyt}
READ(lob_loc { BLOB | CLOB }, amount IN OUT BINARY_INTEGER,
  offset INTEGER, buffer OUT { RAW | VARCHAR2 })
```

**参数**

|参数名称|描述|
|----|--|
|lob loc|指示进行读操作的大对象的位置。|
|amount IN|读取的字节/字符的总数。|
|amount OUT|实际读取的字节或字符的总数。如果这里没有更多数据可供读取，那么参数amount返回0，并且产生异常DATA\_NOT\_FOUND。|
|offset|在大对象中开始进行读操作时的位置。第一个字节或字符的位置是1。|
|buffer|接收大对象内容的变量。如果参数lob\_loc是BLOB类型大对象，那么buffer必须是RAW类型。而如果lob\_loc是一个CLOB类型大对象，那么参数buffer则必须是VARCHAR2类型。|

## SUBSTR {#section_jla_zad_zpc .section}

函数SUBSTR用于返回大对象的部分内容。

``` {#codeblock_3pk_lcf_gfh}
data { RAW | VARCHAR2 } SUBSTR(lob_loc { BLOB | CLOB }
  [, amount INTEGER [, offset INTEGER ]])
```

**参数**

|参数名称|描述|
|----|--|
|lob loc|用于指示进行读操作的大对象的位置。|
|amount|所返回的字节/字符的数量。缺省值是32,767。|
|offset|开始返回数据时在大对象中的位置。第一个字节/字符的位置是1。缺省值是1。|
|data|这个参数用于返回部分被读取的大对象内容。如果参数lob\_loc是BLOB类型大对象，那么buffer必须是RAW类型。而如果参数lob\_loc是一个CLOB类型大对象，那么buffer则必须是VARCHAR2类型。|

## TRIM {#section_dbe_iby_oyf .section}

存储过程TRIM用于将一个大对象截断到指定长度。

``` {#codeblock_k9r_nh8_9g0}
TRIM(lob_loc IN OUT { BLOB | CLOB }, newlen INTEGER)
```

**参数**

|参数名称|描述|
|----|--|
|lob loc|指示被截断长度的大对象的位置。|
|newlen|被截断长度的大对象的字节或字符总数。|

## WRITE {#section_a3t_8o7_t4t .section}

存储过程WRITE用于将数据写到一个大对象中。任何大对象中从指定的偏移量开始，在指定长度范 围内的数据都会被缓冲区中的数据覆盖。

``` {#codeblock_hit_v5l_atu}
WRITE(lob_loc IN OUT { BLOB | CLOB },
  amount BINARY_INTEGER,
  offset INTEGER, buffer { RAW | VARCHAR2 })
```

**参数**

|参数名称|描述|
|----|--|
|lob loc|用于指示进行写操作的大对象的位置。|
|amount|在缓冲区中字节或字符的数量，这些字节或字符将被写到大对象中。|
|offset|从大对象的开始位置算起，以字节/字符为单位的偏移量（起始值是1），写操作从这个偏移量开始执行。|
|buffer|包含要写到大对象中的数据。如果参数lob\_loc是BLOB类型的大对象，那么参数buffer必须是RAW类型。而如果参数lob\_loc是一个CLOB类型的大对象，那么buffer则必须是VARCHAR2类型。|

## WRITEAPPEND {#section_1g1_74p_e27 .section}

存储过程WRITEAPPEND用于将数据添加到一个大对象的末尾。

``` {#codeblock_3q4_ul6_jal}
WRITEAPPEND(lob_loc IN OUT { BLOB | CLOB },
  amount BINARY_INTEGER, buffer { RAW | VARCHAR2 })
```

**参数**

|参数名称|描述|
|----|--|
|lob loc|指示大对象的位置，我们将会把数据添加到这个大对象的末尾。|
|amount|缓冲区中字节或字符的数量，这些字节或字符将添加到大对象的尾部。|
|buffer|要添加到大对象中数据。如果参数lob\_loc所代表的是BLOB类型的大对象，那么参数buffer必须是RAW类型。而如果参数lob\_loc所代表的是一个CLOB类型，那么参数buffer则必须是VARCHAR2类型。|

