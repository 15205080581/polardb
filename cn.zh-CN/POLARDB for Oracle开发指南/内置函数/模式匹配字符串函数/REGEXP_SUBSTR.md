# REGEXP\_SUBSTR {#concept_221663 .concept}

REGEXP\_SUBSTR函数用于为模式搜索字符串，其中模式由与POSIX兼容的正则表达式所指定。REGEXP\_SUBSTR函数返回的字符串与在调用函数中所指定的模式匹配。

## 语法 {#section_ysx_0xu_yhc .section}

``` {#codeblock_w1x_q7n_58n}
TEXT REGEXP_SUBSTR
(
  srcstr        TEXT, 
  pattern       TEXT, 
  position      INT  DEFAULT 1, 
  occurrence    INT  DEFAULT 1,
  modifier      TEXT DEFAULT NULL,
  subexpression INT  DEFAULT 0 
)     
```

## 参数 {#section_6k0_0k2_hh4 .section}

|参数名称|描述|
|----|--|
|srcstr|srcstr指定要搜索的字符串。|
|Pattern|pattern 用于指定REGEXP\_SUBSTR 要搜索的正则表达式。|
|position|position指定表明在源字符串中起始位置的整数值。缺省值为1。|
|occurrence|如果在搜索字符串时， 有一个以上的模式出现，那么occurrence则用于指定返回的匹配信息。缺省值为1.|
|modifier|modifier用于指定控制模式匹配行为的值。缺省值为NULL。关于POLARDB for Oracle所支持的修改器的完整列表，请参见PostgreSQL核心文件，网址如下：[http://www.enterprisedb.com/docs/en/9.3/pg/functions-matching.html](http://www.enterprisedb.com/docs/en/9.3/pg/functions-matching.html)|
|subexpression|subexpression是一个整数值，用于识别由REGEXP\_INSTR返回的pattern部分。subexpression的缺省值为0。 如果我们给subexpression指定一个值，那么在pattern中必须包括一组（或多组）的括号，来孤立正在搜索的值的部分。由subexpression指定的值表明了应被返回的括号组。例如，如果subexpression为2，那么REGEXP\_INSTR将返回第二组括号的位置。

 |

## 示例 {#section_3sb_j38_7hr .section}

在下面的简单示例中，REGEXP\_INSTR搜索的字符串为第一组包含3个连续数字的电话号码：

``` {#codeblock_3ke_kyu_lg9}
edb=# SELECT REGEXP_SUBSTR('800-555-****', '[0-9][0-9][0-9]', 1, 1) FROM DUAL;
 regexp_substr 
---------------
 800
(1 row)        
```

它定位了第一次出现的3个数字，并返回字符串\(8 0 0\)。如果我们要修改命令使其检索第二次出现的三个连续数字，方法如下：

``` {#codeblock_vis_0ch_gq4}
edb=# SELECT REGEXP_SUBSTR('800-555-****', '[0-9][0-9][0-9]', 1, 2) FROM DUAL;
 regexp_substr 
---------------
 555
(1 row)        
```

REGEXP\_SUBSTR返回的555是第二个子字符串的内容。

