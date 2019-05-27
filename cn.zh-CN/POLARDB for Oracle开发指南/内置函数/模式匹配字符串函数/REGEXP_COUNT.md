# REGEXP\_COUNT {#concept_221586 .concept}

REGEXP\_COUNT用于为正则表达式搜索字符串，且返回正则表达式发生的时间信息。

## 语法 {#section_5j0_eg5_4cx .section}

``` {#codeblock_ucs_0w2_qrc}
INTEGER REGEXP_COUNT
(
  srcstr    TEXT,
  pattern   TEXT,
  position  DEFAULT 1
  modifier  DEFAULT NULL
)        
```

## 参数 {#section_yl3_h5k_sgo .section}

|参数名称|描述|
|----|--|
|srcstr|指定要搜索的字符串|
|pattern|指定REGEXP\_COUNT要搜索的正则表达式|
|position|position是一个整数值，用于表明REGEXP\_COUNT要在源字符串中开始搜索的位置。缺省值为1。|
|modifier|modifier用于指定控制模式匹配行为的值。缺省值为NULL。|

**说明：** 关于POLARDB for Oracle所支持的修改器的完整列表，请参见PostgreSQL核心文件，网址如下：[http://www.enterprisedb.com/docs/en/9.3/pg/functions-matching.html](http://www.enterprisedb.com/docs/en/9.3/pg/functions-matching.html)

## 示例 {#section_me3_1od_yi1 .section}

在下列简单示例中，REGEXP\_COUNT返回的是在字符串'reinitializing'中字母i的使用次数：

``` {#codeblock_zqn_w7x_5k3}
edb=# SELECT REGEXP_COUNT('reinitializing', 'i', 1) FROM DUAL;
 regexp_count 
--------------
            5
(1 row)        
```

在第一个示例中，命令了REGEXP\_COUNT开始在首位计数。如果我们要修改指令使其在第六位开始计数，那么就可以：

``` {#codeblock_m8r_mpp_b90}
edb=# SELECT REGEXP_COUNT('reinitializing', 'i', 6) FROM DUAL;
 regexp_count 
--------------
            3
(1 row)            
```

那么REGEXP\_COUNT返回的就是3，且计数结果不包括任何出现在第六位之前的字母i。

