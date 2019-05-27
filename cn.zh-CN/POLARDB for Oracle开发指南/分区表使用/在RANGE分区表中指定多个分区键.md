# 在RANGE分区表中指定多个分区键 {#concept_222036 .concept}

我们可以通过给RANGE分区表指定多个关键列来提高性能。 如果我们经常在小的列集上使用比较运算符（基于大于或小于值）来选择记录，那么可以考虑在RANGE分区规则中使用这些列。

## 在范围分区表中指定多个键 {#section_4it_80u_a5d .section}

在分区键中，范围分区表定义也许包括多个列。要给一个范围分区表指定多个分区键，就要在子句PARTITION BY RANGE之后在逗号分隔的列表中包括列名称：

```
CREATE TABLE sales
(
  dept_no     number,
  part_no     varchar2,
  country     varchar2(20),
  sale_year    number,
  sale_month   number,
  sale_day     number,
  amount      number
)
PARTITION BY RANGE(sale_year, sale_month)
(
  PARTITION q1_2012 
    VALUES LESS THAN(2012, 4),
  PARTITION q2_2012 
    VALUES LESS THAN(2012, 7),
  PARTITION q3_2012 
    VALUES LESS THAN(2012, 10),
  PARTITION q4_2012 
    VALUES LESS THAN(2013, 1)
);
```

如果创建的表有多个分区键，那么我们在查询这个表时必须指定多个键值才能充分利用分区剪枝的优势。

```
acctg=# EXPLAIN SELECT * FROM sales WHERE sale_year = 2012 AND sale_month = 8;
                                   QUERY PLAN                                
----------------------------------------------------------------------------- Result  (cost=0.00..14.35 rows=2 width=250)
   ->  Append  (cost=0.00..14.35 rows=2 width=250)
         ->  Seq Scan on sales  (cost=0.00..0.00 rows=1 width=250)
               Filter: ((sale_year = 2012::numeric) AND (sale_month = 8::numeric))
         ->  Seq Scan on sales_q3_2012 sales  (cost=0.00..14.35 rows=1 width=250)
               Filter: ((sale_year = 2012::numeric) AND (sale_month = 8::numeric))
(6 rows)
```

由于所有在列sale\_month 中值为8 的记录和在列sale\_year 中值为2012 的记录都将存储在分区q3\_2012中，因此POLARDB for Oracle 仅搜索这个分区。

