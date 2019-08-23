# Commands supported for SQL acceleration {#concept_ynp_hmv_4fb .concept}

## Syntax of the SELECT statement {#section_pgn_jmv_4fb .section}

```
[ WITH with_subquery_table_name AS ( query ) ]
SELECT
[DISTINCT] select_expr [, select_expr ...]
[FROM  table_reference [, ...] ]
[WHERE filter_condition]
[GROUP BY { expr [ASC | DESC] | ROLLUP ( expr_list ) | CUBE ( expr_list ) | GROUPING SETS ( expr_list )} , ...]
[HAVING having_condition]
[ORDER BY {col_name | expr }
[ASC | DESC], ...]
[{ UNION [ ALL ] | INTERSECT | EXCEPT } (SELECT select_expr..)]
[LIMIT {[offset,] row_count}]
```

## WITH clause {#section_kjs_tmv_4fb .section}

The WITH clause defines one or more subqueries. Each subquery defines a temporary table, similar to a view definition. These temporary tables can be referenced in other clauses of the current query. All temporary tables defined by the WITH clause can achieve similar results through the subqueries defined in the SELECT statement. However, when these subqueries or temporary tables are referenced by other clauses multiple times, the WITH clause calculates the results only once and reuses the results. This reduces the calculation of common expressions.

**The WITH clause uses the following syntax:**

```
[ WITH with_subquery [, ...] ]
```

The with\_suquery parameter uses the following syntax:

```
with_subquery_table_name AS ( query )
```

**Parameters:**

-   with\_subquery\_table\_name: the name of a unique temporary table in the current query.
-   query: all SELECT queries that are supported.

**Example:**

```
with t as (select x,y from A) select t.y from t order by t.x limit 10
```

## SELECT list {#section_ckz_4mc_pfb .section}

The SELECT list uses the following syntax:

```
SELECT [ ALL | DISTINCT ] * | expression [ AS column_alias ] [, ...]

```

Parameters:

-   `ALL`: an optional redundant field that defines the default behavior if you do not specify `DISTINCT`.
-   `DISTINCT`: deletes duplicate rows.
-   `*`: returns all columns.
-   `expression`: an expression formed from one or more columns, or a column expression that includes one or more functions.
-   `AS column_alias`: the alias of the specified column, where the `AS` keyword is optional. If the **alias** that follows `AS` is a string with space characters, you can enclose it with backquotes \(\`\).
-   If the column name of the table is a keyword, such as `date`, you must enclose it with backquotes \(\`\) to enable the system to parse the column name.

## FROM clause {#section_rcj_rmc_pfb .section}

The FROM clause uses the following syntax:

```
FROM table_reference [, ...]

```

The table\_reference parameter uses the following syntax:

```
with_subquery_table_name [ [ AS ] alias ]
table_name [ * ] [ [ AS ] alias ]
( subquery ) [ AS ] alias
table_reference join_type table_reference
[ ON join_condition ]

```

Parameters:

-   `with_subquery_table_name`: the subquery name defined in the WITH clause.
-   `table_name`: the table of a table or view.
-   `alias`: the alias of a table or view.
-   `join_type`: the type of join.
-   Valid values for `join_type`: \[INNER\] JOIN, LEFT \[OUTER\] JOIN, RIGHT \[OUTER\] JOIN, CROSS JOIN, and NATURAL JOIN.

-   `join_condition`: the join specification where the joining columns are stated as a condition that follows the `ON` keyword. The conditions that follow the `ON` keyword can only be equivalent conditions. Non-equivalent conditions can be defined in the `WHERE` clause.


## WHERE clause {#section_dcs_2sc_pfb .section}

The WHERE clause uses the following syntax:

```
[WHERE filter_condition]

```

The value of the filter\_condition parameter can be multiple expressions connected by binary logical operators such as `AND` and `OR`. It can also be correlated or uncorrelated subqueries \(or Semi Join\) consisting of the `IN`, `NOT IN`, `EXIST`, or `NOT EXIST` operator.

## GROUP BY clause {#section_cvy_fsc_pfb .section}

The GROUP BY clause divides the query result into groups of rows. It uses the following syntax:

```
GROUP BY ([ROLLUP | CUBE] expression [, ...]) | expression [ASC | DESC]

```

The expressions following GROUP BY must be non-aggregate expressions in the SELECT list.

Notes:

-   The GROUP BY alias is supported, such as select x+1 as t from table group by t.
-   The HAVING alias is supported, such as select x+1 as t from table having t \> 10.

-   `GROUP BY col ASC | DESC` is equivalent to `GROUP BY col ORDER BY col ASC | DESC`. When `GROUP BY ASC | DESC` is used together with `ORDER BY`, the query results are sorted by the columns or expressions following `ORDER BY`.

-   If there is a non-aggregate column in the `SELECT` statement, such as the letter a in the statement `SELECT a, count(b) FROM... GROUP BY b`, the non-aggregate column takes the first record returned by GROUP BY.

## HAVING clause {#section_usw_hsc_pfb .section}

The HAVING clause specifies a search condition for a group or an aggregate after grouping. It uses the following syntax:

```
[ HAVING condition ]

```

Notes:

-   The HAVING condition must reference the expression that appears in the columns of the GROUP BY clause, or reference an aggregate expression.
-   The HAVING condition supports column names rather than column aliases in the SELECT list.
-   The HAVING condition does not support subscript references of columns in the SELECT list.

## ORDER BY clause {#section_r2w_ksc_pfb .section}

The ORDER BY clause is used for ordering. It uses the following syntax:

```
[ ORDER BY expression
[ ASC | DESC ]
[ LIMIT { count | ALL } ]

```

Parameters:

-   `expression`: specifies a column or expression as the sort criterion for the query result set. This parameter can be the column or alias in the SELECT list, or be the column that does not appear in the SELECT list.
-   `ASC | DESC`: specifies that the values in the specified column that should be sorted in ascending or descending order. The Null values are treated as the lowest possible values.
-   `LIMIT number | ALL`: limits the number of rows returned. The number parameter specifies the number of rows, and ALL specifies that all rows are returned.

**Note:** LIMIT supports offset, such as `LIMIT n, m`.

## UNION, INTERSECT, EXCEPT, and MINUS clauses {#section_yx4_nsc_pfb .section}

The UNION, INTERSECT, EXCEPT, and MINUS clauses are used to perform set operations including union, intersection, and difference. They use the following syntax:

```
query
{ UNION [ ALL ] | INTERSECT | EXCEPT | MINUS }
query

```

Parameters:

-   `query`: The query parameter must return the consistent number and type of columns prior to and following the operators.
-   `UNION [ALL]`: returns the result of performing the union operation on query result sets. The ALL parameter specifies that deduplication is not required.
-   `INTERSECT`: returns the result of performing the intersection operation on query result sets.
-   `EXCEPT`: returns the result of the difference operation on query result sets.
-   `MINUS`: returns the result of the difference operation on query result sets. The effect is the same as `EXCEPT`.

Order of the set operations:

Both the `UNION` and `EXCEPT` operators are left-associative. For example:

```
select * from t1
unionselect * from t2
exceptselect * from t3
orderby c1;

```

In this statement, the operations t1 union t2 except t3 are finished first, followed by global sorting of the preceding operation result according to c1.

The `INTERSECT` operator is prior to `UNION` and `EXCEPT`. For example:

```
select * from t1
unionselect * from t2
intersectselect * from t3
orderby c1;

```

The preceding statement is equivalent to the following statement:

```
select * from t1
union
(select * from t2
intersectselect * from t3)
orderby c1;

```

**Note:** The query result set prior to a set operator cannot contain the ORDER BY statement. If the ORDER BY statement is required, enclose the statement in parentheses.

