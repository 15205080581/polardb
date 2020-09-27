# Parallel Hint

Parallel Hints可以指定优化器是否选择并行执行，还支持指定并行度以及需要并行的表。Parallel Hints目前包含`PARALLEL`和`NO_PARALLEL`两种Hints。

## 前提条件

PolarDB集群版本需为PolarDB MySQL 8.0且Revision version为8.0.1.0.5或以上，您可以参见[查询版本号](/cn.zh-CN/.md)确认集群版本。

## PARALLEL Hint

您可以使用如下语法通过PARALLEL Hint强制query并行执行，以及指定并行度或要并行的表：

```
/*+ parallel [( [query_block] [table_name]  [degree] )] */
```

示例

-   强制query并行执行：

    ```
    SELECT /*+PARALLEL()*/ * FROM t1, t2;
    ```

-   强制query以并行度8执行：

    ```
    SELECT /*+PARALLEL(8)*/ * FROM t1, t2;
    ```

-   强制query并行且选择t1表并行：

    ```
    SELECT /*+PARALLEL(t1)*/ * FROM t1, t2;
    ```

-   强制query选择t1表并行且以并行度8执行：

    ```
    SELECT /*+PARALLEL(t1 8)*/ * FROM t1, t2;
    ```


**说明：**

-   并行度最大可以被设置为1024。
-   仅支持指定一个表并行。
-   若目标表不存在，则Hint会被忽略且会出现`Warning`提示。
-   若目标表不可以并行，则Hint会被忽略。

## NO\_PARALLEL hint

您可以使用如下语法通过NO\_PARALLEL Hint强制query串行执行，或者指定禁止某些表并行访问：

-   强制query串行执行：

    ```
    SELECT /*+NO_PARALLEL()*/ * FROM t1, t2;
    ```

-   禁止t1表并行访问：

    ```
    SELECT /*+NO_PARALLEL(t1)*/ * FROM t1, t2;
    ```

-   同时禁止t1,t2表并行访问：

    ```
    SELECT /*+NO_PARALLEL(t1, t2)*/ * FROM t1, t2;
    ```


**说明：**

-   若目标表不存在，则Hint会被忽略且会出现`Warning`提示。
-   若所有的表禁止并行访问，等价于强制query串行执行。

