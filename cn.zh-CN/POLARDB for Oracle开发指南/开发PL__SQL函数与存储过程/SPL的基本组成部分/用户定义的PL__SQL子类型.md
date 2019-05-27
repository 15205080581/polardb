# 用户定义的PL/SQL子类型 {#concept_222099 .concept}

POLARDB for Oracle支持由用户定义的PL/SQL子类型和 \(子类型\) 别名。 子类型是一个带有可选约束集合的数据类型，其中约束集合用于限制存储在这个类型列中的值。对于适用于有子类型的数据类型的规则仍然是要执行的，但是我们可以使用额外的约束条件来限定存储在类型中的值的精度或范围。

我们可以在PL函数、存储过程、匿名代码块或包的声明中定义一个子类型。语法如下：

``` {#codeblock_en2_lu0_wk7}
SUBTYPE subtype_name IS type_name[(constraint)] [NOT NULL] 
```

其中constraint是：

``` {#codeblock_shd_8as_37k}
{precision [, scale]} | length
```

其中：

-   subtype\_name：指定子类型的名称。
-   type name：type\_name 指定子类型所基于的原始类型的名称。

    **说明：** type\_name 可以是以下几种名称：

    -   支持的任何类型的名称。
    -   任何合成类型的名称。
    -   由%TYPE运算符固定的列。
    -   另一个子类型的名称。

使用constraint子句来给支持精度或范围的类型定义限制条件。

-   precision：用于指定子类型值中允许的数字的总数。
-   scale：用于指定子类型值中允许的小数的数量。
-   length：用于指定CHARACTER、VARCHAR、或 TEXT基本类型的值允许的总长度。

我们可以包括NOT NULL子句来指定NULL值可以不存储在所指定子类型的列中。

**说明：** 一个基于列的子类型将继承列的尺寸约束条件，但不会继承NOT NULL或CHECK的约束条件。

## 无约束的子类型 {#section_wjs_zwm_brj .section}

要创建无约束的子类型，可以使用SUBTYPE命令来指定新的子类型名称和子类型所基于的原始类型的名称。例如，下列命令创建了一个名为address的子类型，且具有类型CHAR所有的属性：

``` {#codeblock_gqy_1y5_v1g}
SUBTYPE address IS CHAR;
```

我们也可以创建这样一个子类型（约束的或无约束的），它是另一个子类型的子类型：

``` {#codeblock_2mm_ux3_9nm}
SUBTYPE cust_address IS address NOT NULL;
```

上述命令所创建的名为cust\_address的子类型共享了子类型address的所有属性。 我们可以包括NOT NULL子句来指定子类型cust\_address的值不为NULL空值。

## 约束的子类型 {#section_7hb_nms_kn6 .section}

当我们创建一个基于字符类型的子类型时， 可以包括length值来定义所创建子类型的最大长度。例如：

``` {#codeblock_wo9_2yt_ayu}
SUBTYPE acct_name IS VARCHAR (15);
```

上述示例创建的名为acct\_name的子类型是基于数据类型VARCHAR上的，但它的最大长度限制为15个字符。

我们可以为precision包括一个值（来指定子类型值中的最多数字数量）。当约束一个数值基础类型时，也可以选择性的包括scale（来指定小数点右侧的数字数量）。例如：

``` {#codeblock_039_gva_73d}
SUBTYPE acct_balance IS NUMBER (5, 2);
```

上述示例创建的名为acct\_balance的子类型共享了类型NUMBER的所有属性，但它小数点左侧不能超过3个数字，小数点右侧不能超过2个数字。

参数的声明（在函数标头或存储过程标头中）就是形参。传递到函数或存储过程的值就是实际参数。 当调用函数或存储过程时，调用者会提供（0或更多的）实际参数。每个实际参数会被分配到一个可以约束函数主体或存储过程主体值的形参中。

如果我们把一个形参声明为一个约束的子类型，那么：

-   当调用一个函数且把一个实际参数分配到一个形参中时，POLARDB for Oracle不会执行子类型约束。
-   当调用一个存储过程且把一个实际参数分配到一个形参中时，POLARDB for Oracle会执行子类型约束。

## 使用%TYPE运算符 {#section_arg_1na_xpn .section}

我们可以使用%TYPE符号来声明一个链接到列中的子类型。例如：

``` {#codeblock_9yk_gzb_6in}
SUBTYPE emp_type IS emp.empno%TYPE
```

上述这条命令创建了名为emp\_type子类型，且它的基础类型与表emp中empno列的类型相匹配。一个基于列的子类型将共享列的尺寸约束，但不会继承NOT NULL和CHECK约束条件。

## 子类型的转换 {#section_mmz_hmp_sna .section}

无约束的子类型是它们所基于的类型的别名。在不进行转换的前提下，任何类型、子类型（无约束的）的变量都能够和基础类型的变量相互转换。反之亦然。

在不进行转换的前提下，一个约束的子类型变量能够和基础类型的变量相互转换。但是，如果当基础类型和子类型的约束条件一致时，那么基础类型变量只能够和一个约束的子类型相互转换。一个约束的子类型变量可以隐式地转换为另一个子类型，但前提必须是它们基于相同的子类型之上，而且约束值必须在要转换的子类型值的范围内。

