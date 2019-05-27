# SPL的基本组成部分 {#concept_222078 .concept}

本节讨论了开发一个SPL程序所需要最基本的组成部分。

## 字符集 {#section_f40_8t8_88w .section}

SPL程序使用到下面这些字符：

-   大写字母A到Z，小写字母a到z
-   数字0到9
-   符号\( \) + - \* / < \> = ! ~ ^ ; : . ' @ % , " \# $ & \_ | \{ \} ? \[ \]
-   Tab键，空格字符和回车键

SPL语言所包含的标识符，表达式，语句，控制流程结构使用上面这些字符组成的。

**说明：** SPL程序可以操作的数据是由数据库编码所支持的字符集决定。

## 大小写处理 {#section_e5j_pmp_qgo .section}

从下面这个示例中可以看到：在SPL程序中使用的关键字和用户定义的标识符是不区分大小写的。

示例：

``` {#codeblock_cx9_cpq_j1u}
DBMS_OUTPUT.PUT_LINE('Hello World');
```

可以等同于下面这些语句：

``` {#codeblock_x08_c15_yf9}
dbms_output.put_line('Hello World');
```

``` {#codeblock_12d_q25_eng}
Dbms_Output.Put_Line('Hello World');
```

``` {#codeblock_f2a_mxt_4ia}
DBMS_output.Put_line('Hello World');
```

但是，字符和字符串常量, 以及任何从POLARDB for Oracle数据库或外部数据源所取得数据是区分大小写的。语句`DBMS_OUTPUT.PUT_LINE('Hello World!')；`产生了如下的输出：

``` {#codeblock_xez_6ks_4gu}
Hello World!
```

但是语句DBMS\_OUTPUT.PUT\_LINE\('HELLO WORLD!'\)；的输出着这样的：

``` {#codeblock_2lj_8tn_fmt}
HELLO WORLD!
```

## 标识符 {#section_1av_vqf_jz1 .section}

标识符是用户定义的名称，用来标识组成SPL程序的各个部分，包括变量,游标,标签,程序和参数。

在SPL中有效标识符的语法规则与在SQL语言中的规则是一样的。

一个标识符不能定义为与SPL语言和SQL语言中关键字相同名字。下面这些示例是一些正确定义的标识符。

``` {#codeblock_dx4_nth_ji2}
x
last    name
a_$_Sign
Many$$$$$$$$signs    
THIS_IS_AN_EXTREMELY_LONG_NAME A1                
```

## 限定词 {#section_t6r_kuy_0y3 .section}

限定词是一个指定对象的所有者或者是使用这个对象时所在环境的名称。所谓对象就是属于限定词实体的名称。通常来说， 一个限定词拥有的实体就是一个限定词后面跟随一个英文句号（.）， 后面再跟着这个限定词所拥有对象的名称。要注意的是'.'的前后都没有空格。这个句法叫做dot notation。

下面就是引用被限定的对象的语法。

``` {#codeblock_o5a_18t_q2i}
qualifier. [ qualifier. ]... object
```

qualifier是对象的所有者。object就是属于限定词的实体的名称。有一种情况是前一个限定词所拥有的实体，会被这个实体之后限定词和对象标识为限定词。

几乎所有的标识符都可以被限定。一个标识符是否可以被限定取决于标识符所表示的含义和使用这个标识符的环境。

下面是一些限定词的示例。

-   由存储过程和函数所属的模式来限定的名称 - 例如，schema\_name.procedure\_name
-   由触发器所属的模式来限定的名称 - 例如，schema\_name.trigger\_name
-   由列所属的数据表来限定的列名 - 例如，emp.empno
-   由数据表所属的模式来限定的表名称 – 例如，public. emp
-   由数据表和模式所限定的列名 - 例如， public.emp.empno

一条通用的规则是，无论在一个SPL语句语法中的任何地方出现名称， 它的被限定名称也都会被用到。

通常来说当像名称相同且属于两个不同的模式的两个存储过程在一个程序中被调用， 或者在一个程序中SPL变量和一个数据表的列相同等这样的标识符命名冲突的情况出现时，会用到被限定的名称。

在实际应用中建议应该尽量避免使用限定词。在本章中，我们可以使用下面这些书写约定来避免命名冲突：

-   在SPL程序声明的所有的变量以v\_的前缀开头。 例如， v\_empno
-   在存储过程过程或者函数中定义的参数以p\_的前缀开头。例如，p\_empno
-   列名和表名不用特定的前缀开头。例如，在数据表emp中的列名empno

## 常量 {#section_6gi_218_sq6 .section}

在SPL程序中可以使用常量（或称为直接变量）表示不同数据类型的值。例如-数值，字符串，日期等。常量一般可以是下面这些类型：

-   数值（包括整型和实数型）
-   字符和字符串
-   日期/时间

