# XML 类型 {#concept_221048 .concept}

XMLTYPE数据类型用于存储XML数据。 这个数据类型在存储XML数据时的优点在于，它能够检查输入值的结构完整性，而且还有函数来支持类型安全的操作。

就像XML标准定义的一样，XML类型能够存储结构完整的“文件”。同时XML 类型也可以存储碎片“内容”，XML标准中的XMLDecl? Content生成对此做了定义。大致地说，这就意味着内容碎片能有一个以上最高级的成员或字符节点。

**说明：** Oracle不支持存储XMLTYPE列中的内容碎片。

## 示例 {#section_2jr_95y_5w0 .section}

下列示例显示了向含有XMLTYPE列的表创建及插入一条记录。

``` {#codeblock_50d_q1n_m0b}
CREATE TABLE books (
    content         XMLTYPE
);

INSERT INTO books VALUES (XMLPARSE (DOCUMENT '<?xml version="1.0"?><book><title>Manual</title><chapter>...</chapter></book>'));

SELECT * FROM books;

                         content
----------------------------------------------------------
 <book><title>Manual</title><chapter>...</chapter></book>
(1 row)			
```

