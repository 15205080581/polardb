# 位置参数符号 vs 命名参数符号 {#concept_222145 .concept}

当把参数传递给一个函数或存储过程时，我们既可以使用位置参数符号也可以使用命名参数符号。如果使用位置符号指定参数，那么我们必须按照声明参数的顺序列出参数。如果我们使用命名符号指定参数的话，参数的顺序就不重要了。

使用命名符号来指定参数时，列出每个参数的名称，后面加上箭头\(=\>\)和参数值。相对来说，命名符号更为冗长一些，但使用命名符号指定的参数代码更为简单易读，便于维护。

## 案例演示 {#section_8bt_l4b_fcm .section}

下列的简单示例中，分别演示了位置参数符号和命名参数符号的使用。

```
CREATE OR REPLACE PROCEDURE emp_info (
    p_deptno        IN     NUMBER,
    p_empno         IN OUT NUMBER,
    p_ename         IN OUT VARCHAR2,
)
IS
BEGIN
    dbms_output.put_line('Department Number =' || p_deptno);
    dbms_output.put_line('Employee Number =' || p_empno);
    dbms_output.put_line('Employee Name =' || p_ename;
END;
```

如果使用位置符号调用存储过程，就按照如下所示进行操作：

``` {#codeblock_1lt_5d6_v4g}
emp_info(30, 7455, 'Clark'); 
```

如果使用命名符号调用存储过程，就按照如下所示进行操作：

``` {#codeblock_f5r_mlr_xij}
emp info(p ename =>'Clark', p empno=>7455, p deptno=>30);
```

如果在参数列表发生改变时、重新排序参数时或新添加一个可选参数时，使用命名符号可以减少重新编排存储过程参数列表的需要。

如果在我们给参数设定一个缺省值时，或者这个参数并不是末尾参数时，那么我就必须使用命名符号来调用存储过程或函数。下列示例中的存储过程带有两个主要的缺省参数。

```
CREATE OR REPLACE PROCEDURE check_balance (
    p_customerID  IN NUMBER DEFAULT NULL,
    p_balance     IN NUMBER DEFAULT NULL,
    p_amount      IN NUMBER
)
IS 
DECLARE  
    balance NUMBER;
BEGIN
   IF (p_balance IS NULL AND p_customerID IS NULL) THEN
      RAISE_APPLICATION_ERROR 
          (-20010, 'Must provide balance or customer');
   ELSEIF (p_balance IS NOT NULL AND p_customerID IS NOT NULL) THEN
      RAISE_APPLICATION_ERROR 
          (-20020,'Must provide balance or customer, not both');
   ELSEIF (p_balance IS NULL) THEN
      balance := getCustomerBalance(p_customerID);
   ELSE 
      balance := p_balance;
   END IF;

   IF (amount > balance) THEN
      RAISE_APPLICATION_ERROR 
        (-20030, 'Balance insufficient');
   END IF;
END;
```

通过使用命名符号，我们只能忽略非末尾参数值（当我们调用这个存储过程时）。当使用位置符号时，我们只能缺省末尾参数。我们可以通过使用下列参数来调用这个存储过程：

-   ```
check_balance(p_customerID => 10, p_amount = 500.00)
```

-   ```
check_balance(p_balance => 1000.00, p_amount = 500.00)
```


我们可以通过结合位置符号和命名符号的方法（混合符号）来指定参数。下列简单示例为混合参数符号的使用方法：

```
CREATE OR REPLACE PROCEDURE emp_info (
    p_deptno        IN     NUMBER,
    p_empno         IN OUT NUMBER,
    p_ename         IN OUT VARCHAR2,
)
IS
BEGIN
    dbms_output.put_line('Department Number =' || p_deptno);
    dbms_output.put_line('Employee Number =' || p_empno);
    dbms_output.put_line('Employee Name =' || p_ename;
END;
```

我们可以通过混合符号来调用存储过程：

``` {#codeblock_0xl_isl_0n0}
emp info(30, p ename =>'Clark', p empno=>7 4 55);
```

如果我们使用了混合符号来调用存储过程，那么命名参数绝对不能优先于位置参数。

