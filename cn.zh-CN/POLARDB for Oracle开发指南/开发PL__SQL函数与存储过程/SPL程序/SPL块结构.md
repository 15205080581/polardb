# SPL块结构 {#concept_222107 .concept}

对于一个SPL程序来说，无论是存储过程，函数或者触发器， 它的代码块结构都是相同的。一个代码块由三个部分组成-一个可选的变量声明部分，一个必选的命令执行部分，和一个可选的捕获异常部分。一个最简单的代码块由命令执行部分构成，包含一条或多条写在关键字BEGIN和END中间的代码块中可以有一个可选的变量声明部分，用来声明那些在执行和捕获异常部分中使用到的变量，游标和类型。

声明部分是在执行部分中BEGIN关键字前面出现。声明部分以关键词DECLARE开始，这取决于当时使用代码块的情况。

最后，在BEGIN-END块里面可以有一个可选的，用于捕获异常的部分。 捕获异常的部分以关键字EXCEPTION开始，在代码块的结束位置结束。如果在代码块中的一条语句产生了一个异常，程序控制流程就会转到捕获异常的部分，在这个部分中是否对异常进行处理取决于异常和异常处理流程的内容。

下面就是一个代码块的通用结构。

``` {#codeblock_pkp_u94_4h3}
[ [ DECLARE ]
      declarations ]
    BEGIN
      statements
  [ EXCEPTION
      WHEN exception_condition THEN
        statements [, ...] ]
    END;
```

**说明：** 

-   declarations是指在代码块中的一个或多个变量，游标或类型的声明。 每一个声明必须以一个分号结束。关键字DECLARE的使用取决于在代码块所出现的环境。
-   statements是一条或多条的SPL语句。每一条语句必须以一个分号结束。以关键词END标识的块结束的位置也要以分号结束。

代码块中出现的关键字EXCEPTION表示捕获异常部分的开始。exception\_condition是指用来测试一种或多种类型异常的条件表达式。如果一个产生的异常与exception\_condition中一个异常类型相匹配， 那么将执行跟随在WHEN exception\_condition子句后面的statements。这里可以有一个或多个WHEN exception\_condition子句， 每一个子句后面都会跟随相应的语句。

**说明：** 一个BEGIN/END块本身就是一个语句，因此代码块是可以嵌套的。捕获异常部分可以包含嵌套的代码块。

下面是一个示例，这是一个最简单的代码块。 在这个代码块中的执行部分包含了一个NULL语句，NULL语句是一个可执行的语句中，不做任何工作。

``` {#codeblock_3oj_wo0_8rl}
BEGIN
    NULL;
END;
```

下面这个代码块包含了变量声明和命令执行这两个部分。

``` {#codeblock_bdy_2pg_kuw}
DECLARE
    v_numerator     NUMBER(2);
    v_denominator   NUMBER(2);
    v_result        NUMBER(5,2);
BEGIN
    v_numerator := 75;
    v_denominator := 14;
    v_result := v_numerator / v_denominator;
    DBMS_OUTPUT.PUT_LINE(v_numerator || ' divided by ' || v_denominator ||
        ' is ' || v_result);
END;
```

在上面的示例中，首先将3个数值变量声明为NUMBER数据类型，在执行部分中对两个变量分配了数值， 然后使其中一个数值被另外一个数值整除。所得的结果存放在第三个变量中， 最后使用第三个变量用来显示结果。执行这个代码块的输出如下所示：

``` {#codeblock_4cr_bql_nux}
75 divided by 14 is 5.36
```

在下面的示例中显示了一个代码块，它包含了变量声明， 命令执行和捕获异常这三个部分。

``` {#codeblock_otk_rrc_2ob}
DECLARE
    v_numerator     NUMBER(2);
    v_denominator   NUMBER(2);
    v_result        NUMBER(5,2);
BEGIN
    v_numerator := 75;
    v_denominator := 0;
    v_result := v_numerator / v_denominator;
    DBMS_OUTPUT.PUT_LINE(v_numerator || ' divided by ' || v_denominator ||
        ' is ' || v_result);
    EXCEPTION
        WHEN OTHERS THEN
            DBMS_OUTPUT.PUT_LINE('An exception occurred');
END;
```

下面的这个输出结果显示了当代码块中的执行了除零操作时，在捕获异常部分中执行相关语句的结果。

``` {#codeblock_a3g_7vo_xvs}
An exception occurred
```

