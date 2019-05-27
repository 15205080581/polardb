# REGEXP\_INSTR {#concept_221648 .concept}

REGEXP\_INSTR用于为POSIX式的正则表达式搜索字符串。这个函数返回的是字符串中的匹配内容的位置信息。

## 语法 {#section_m38_jjg_q50 .section}

``` {#codeblock_swo_o68_18o}
INTEGER REGEXP_INSTR
(
  srcstr        TEXT, 
  pattern       TEXT, 
  position      INT  DEFAULT 1,
  occurrence    INT  DEFAULT 1,
  returnparam   INT  DEFAULT 0,
  modifier      TEXT DEFAULT NULL,
  subexpression INT  DEFAULT 0,
)         
```

## 参数 {#section_7pj_xc3_gqe .section}

|参数名称|描述|
|----|--|
|srcstr|srcstr指定要搜索的字符串。|
|pattern|pattern指定REGEXP\_INSTR 函数要搜索的正则表达式。|
|position|position指定表明在源字符串中起始位置的整数值。缺省值为1。|
|occurrence|如果在搜索字符串时， 有一个以上的模式出现，那么occurrence则用于指定返回的匹配信息。缺省值为1.|
|returnparam|returnparam是一个整数值，用于指定REGEXP\_INSTR应该返回的字符串中的位置。缺省值为0。可以指定下列内容： -   指定0来返回字符串中第一个与pattern匹配的字符位置。
-   指定一个大于0的值来返回pattern结尾后的第一个字符位置。

 |
|modifier|modifier用于指定控制模式匹配行为的值。缺省值为NULL。关于POLARDB for Oracle所支持的修改器的完整列表，请参见PostgreSQL核心文件，网址如下：[http://www.enterprisedb.com/docs/en/9.3/pg/functions-matching.html](http://www.enterprisedb.com/docs/en/9.3/pg/functions-matching.html)|
|subexpression|subexpression是一个整数值，用于识别由REGEXP\_INSTR返回的pattern部分。subexpression的缺省值为0。 如果我们给subexpression指定一个值，那么在pattern中必须包括一组（或多组）的括号，来孤立正在搜索的值的部分。由subexpression指定的值表明了应被返回的括号组。例如，如果subexpression为2，那么REGEXP\_INSTR将返回第二组括号的位置。

 |

## 示例 {#section_t4u_aup_367 .section}

在下列简单的示例中，REGEXP\_INSTR用于搜索包含电话号码的字符串。 这个字符串为第一次出现的包含3个连续数字的模式：

``` {#codeblock_ugb_5o0_otx}
edb=# SELECT REGEXP_INSTR('800-555-1212', '[0-9][0-9][0-9]', 1, 1) FROM DUAL;
 regexp_instr 
--------------
            1
(1 row)        
```

示例中命令了REGEXP\_INSTR返回第一次出现的位置。如果我们要修改命令使其返回三个连续数字的第二次出现的起始位置，方法如下：

``` {#codeblock_0ug_dlm_ify}
edb=# SELECT REGEXP_INSTR('800-555-1212', '[0-9][0-9][0-9]', 1, 2) FROM DUAL;
 regexp_instr 
--------------
            5
(1 row)        
```

