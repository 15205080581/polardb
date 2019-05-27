# 使用LIKE操作符进行模式匹配 {#concept_221676 .concept}

POLARDB for Oracle提供的模式匹配功能是通过使用传统的SQL LIKE操作符来实现的。LIKE操作符的使用语法如下所示。

``` {#codeblock_mgs_jf6_v7o}
string LIKE pattern [ ESCAPE escape-character ]
string NOT LIKE pattern [ ESCAPE escape-character ]
```

每个参数pattern都定义了一个字符串集，如果参数pattern定义的字符串集中包含参数string的值，那么LIKE表达式返回true.正如所期望的，如果LIKE表达式返回为真，那么NOT LIKE表达式返回为假，反之亦然。与NOT LIKE相等的表达式是NOT \(string LIKE pattern\)。

如果参数pattern不包括百分号或者下划线，那么模式只表示字符串本身，在这种情况下，LIKE操作符和等于号的作用相同。在参数pattern中的下划线表示匹配单个字符，而百分号则表示匹配任意字符串。

**示例：**

``` {#codeblock_gyb_kx2_8se}
'abc' LIKE 'abc'    true
'abc' LIKE 'a%'     true
'abc' LIKE '_b_'    true
'abc' LIKE 'c'      false    
```

LIKE模式匹配覆盖整个字符串，如果想从字符串中任意位置开始匹配，那么模式必须以百分号开始，以百分号结束。

如果只想匹配字符串中的下划线或者百分号，那么在模式中，必须通过使用换码符对这两个字符分别进行处理。缺省的换码符是反斜线，但是我们也可以通过使用ESCAPE子句来选择一个不同的换码符。如果想匹配换码符本身，那么就需要写上两个换码符。

需要注意的是在字符串中，反斜线已经有了特定含义，所以当匹配模式中包含一个反斜线的时候，在SQL语句中实际上要写上2个反斜线。因此，书写一个包含以文字方式出现的反斜线意味着必须在语句中写上4个反斜线。而通过使用ESCAPE子句来选择不同的换码符，就可以避免这种情况的发生；这样反斜线对于LIKE操作符来说就没有特定的含义了（但是对于字符串分析器来说，它仍然具有特定含义，所以需要在字符串中写2个反斜线。） 。

我们也可以通过使用ESCAPE ‘’来不选择换码符。这样可以有效地禁用换码符机制，使其不可能 关闭匹配模式中的下划线和百分号的特定含义。

