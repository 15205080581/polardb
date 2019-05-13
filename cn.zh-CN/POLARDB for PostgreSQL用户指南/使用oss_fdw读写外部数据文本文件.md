# 使用oss\_fdw读写外部数据文本文件 {#concept_264443 .concept}

阿里云支持通过oss\_fdw插件将OSS中的数据加载到POLARDB for PostgreSQL数据库中，也支持将POLARDB for PostgreSQL数据库中的数据写入OSS中。

## oss\_fdw 参数 {#section_cvf_43g_wdb .section}

oss\_fdw和其他fdw接口一样，对外部数据OSS中的数据进行封装。用户可以像使用数据表一样通过oss\_fdw读取OSS中存放的数据。oss\_fdw提供独有的参数用于连接和解析OSS上的文件数据。

**说明：** 

-   目前oss\_fdw支持读取和写入OSS中文件的格式为：text/csv、gzip格式的text/csv文件。
-   oss\_fdw各参数的值需使用双引号（""）引起来，且不含无用空格。

## CREATE SERVER 参数 {#section_smy_p3g_wdb .section}

-   ossendpoint：是内网访问OSS的地址，也称为host。
-   id oss：账号id。
-   key oss：账号key。
-   bucket： OSSBucket，需要先创建OSS账号再设置该参数。

针对导入模式和导出模式，提供下列容错相关参数。网络条件较差时，可以调整以下参数，以保障导入和导出成功。

-   oss\_connect\_timeout：设置链接超时，单位秒，默认是10秒。
-   oss\_dns\_cache\_timeout：设置DNS超时，单位秒，默认是60秒。
-   oss\_speed\_limit：设置能容忍的最小速率，默认是1024，即1K。
-   oss\_speed\_time：设置能容忍最小速率的最长时间，默认是15秒。

如果使用了oss\_speed\_limit和oss\_speed\_time的默认值，表示如果连续15秒的传输速率小于1K，则超时。

## CREATE FOREIGN TABLE参数 {#section_hhj_r3g_wdb .section}

-   filepath： OSS中带路径的文件名。

    -   文件名包含文件路径，但不包含bucket。

    -   该参数匹配OSS对应路径上的多个文件，支持将多个文件加载到数据库。

    -   文件命名为filepath和filepath.x 支持被导入到数据库，x要求从1开始，且连续。

        例如，filepath、filepath.1、filepath.2、filepath.3、filepath.5 ，前4个文件会被匹配和导入，但是 filepath.5将无法导入。

-   dir：OSS中的虚拟文件目录。

    -   dir需要以/结尾。

    -   dir指定的虚拟文件目录中的所有文件（不包含子文件夹和子文件夹下的文件）都会被匹配和导入到数据库。

-   prefix：指定数据文件对应路径名的前缀，不支持正则表达式，且与 filepath、dir 互斥，三者只能设置其中一个。
-   format：指定文件的格式，目前只支持csv。

-   encoding：文件中数据的编码格式，支持常见的pg编码，如utf8。

-   parse\_errors：容错模式解析，以行为单位，忽略文件分析过程中发生的错误。

-   delimiter：指定列的分割符。

-   quote：指定文件的引用字符。

-   escape：指定文件的逃逸字符。

-   null：指定匹配对应字符串的列为null，例如null ‘test’，即列值为’test’的字符串为null。

-   force\_not\_null：指定某些列的值不为null。例如，force\_not\_null ‘id’表示：如果id列的值为空，则该值为空字符串，而不是null。

-   compressiontype：设置读取和写入OSS上文件的的格式：

    -   none：默认的文件类型，即没有压缩的文本格式。
    -   gzip：读取文件的格式为gzip压缩格式。
-   compressionlevel：设置写入OSS的压缩格式的压缩等级，范围1到9，默认6。


**说明：** 

-   filepath和dir需要在OPTIONS参数中指定。
-   filepath和dir必须指定两个参数中的其中一个，且不能同时指定。
-   导出模式目前只支持虚拟文件夹的匹配模式，即只支持dir，不支持filepath。

## CREATE FOREIGN TABLE的导出模式参数 {#section_sxg_t3g_wdb .section}

-   oss\_flush\_block\_size：单次刷出到OSS的buffer大小，默认32MB，可选范围1到128MB。

-   oss\_file\_max\_size：写入OSS的最大文件大小，超出之后会切换到另一个文件续写。默认1024MB，可选范围8到4000 MB。

-   num\_parallel\_worker：写OSS数据的压缩模式中并行压缩线程的个数，范围1到8，默认并发数3。


## 辅助函数 {#section_uw1_x3g_wdb .section}

FUNCTION oss\_fdw\_list\_file \(relname text, schema text DEFAULT ‘public’\)

-   用于获得某个外部表所匹配的OSS上的文件名和文件的大小。

-   文件大小的单位是字节。


```
select * from oss_fdw_list_file('t_oss');
              name              |   size    
--------------------------------+-----------
 oss_test/test.gz.1  | 739698350
 oss_test/test.gz.2  | 739413041
 oss_test/test.gz.3  | 739562048
(3 rows)
```

## 辅助功能 {#section_tn2_z3g_wdb .section}

oss\_fdw.rds\_read\_one\_file：在读模式下，指定某个外表匹配的文件。设置后，该外部表在数据导入中只匹配这个被设置的文件。

例如，set oss\_fdw.rds\_read\_one\_file = ‘oss\_test/example16.csv.1’;

```
set oss_fdw.rds_read_one_file = 'oss_test/test.gz.2';
select * from oss_fdw_list_file('t_oss');
              name              |   size    
--------------------------------+-----------
  oss_test/test.gz.2  | 739413041
(1 rows)
```

## oss\_fdw用例 {#section_pgb_bjg_wdb .section}

```
# 创建插件
create extension oss_fdw; 
# 创建 server 
CREATE SERVER ossserver FOREIGN DATA WRAPPER oss_fdw OPTIONS 
     (host 'oss-cn-hangzhou.aliyuncs.com' ， id 'xxx'， key 'xxx'，bucket 'mybucket');
# 创建 oss 外部表
CREATE FOREIGN TABLE ossexample 
    (date text， time text， open float，
     high float， low float， volume int) 
     SERVER ossserver 
     OPTIONS ( filepath 'osstest/example.csv'， delimiter '，' ，
         format 'csv'， encoding 'utf8'， PARSE_ERRORS '100');
# 创建表，数据就装载到这张表中
create table example
        (date text， time text， open float，
         high float， low float， volume int);
# 数据从 ossexample 装载到 example 中。
insert into example select * from ossexample;
# 可以看到
# oss_fdw 能够正确估计 oss 上的文件大小，正确的规划查询计划。
explain insert into example select * from ossexample;
                             QUERY PLAN                              
---------------------------------------------------------------------
 Insert on example  (cost=0.00..1.60 rows=6 width=92)
   ->  Foreign Scan on ossexample  (cost=0.00..1.60 rows=6 width=92)
         Foreign OssFile: osstest/example.csv.0
         Foreign OssFile Size: 728
(4 rows)
# 表 example 中的数据写出到 OSS 中。
insert into ossexample select * from example;
explain insert into ossexample select * from example;
                           QUERY PLAN
-----------------------------------------------------------------
 Insert on ossexample  (cost=0.00..16.60 rows=660 width=92)
   ->  Seq Scan on example  (cost=0.00..16.60 rows=660 width=92)
(2 rows)
```

## oss\_fdw 注意事项 {#section_frx_cjg_wdb .section}

-   oss\_fdw是在PostgreSQL FOREIGN TABLE框架下开发的外部表插件。

-   数据导入的性能和POLARDB for PostgreSQL集群的资源（CPU IO MEM MET）相关，也和OSS相关。

-   为保证数据导入的性能，请确保云数据库POLARDB for PostgreSQL与OSS所在Region相同，相关信息请参考[OSS endpoint 信息](https://help.aliyun.com/document_detail/oss/user_guide/oss_concept/endpoint.html)。

-   如果读取外表的SQL时触发 ERROR: oss endpoint userendpoint not in aliyun white list, 建议使用[阿里云各可用区公共 endpoint](https://help.aliyun.com/document_detail/31837.html)。如果问题仍无法解决，请通过工单反馈。


## 错误处理 {#section_owy_djg_wdb .section}

导入或导出出错时，日志中会出现下列错误提示信息：

-   code：出错请求的HTTP状态码。

-   error\_code：OSS的错误码。

-   error\_msg：OSS的错误信息。

-   req\_id：标识该次请求的UUID。当您无法解决问题时，可以凭req\_id来请求OSS开发工程师的帮助。


请参考以下链接中的文档了解和处理各类错误，超时相关的错误可以使用oss\_ext相关参数处理。

-   [OSS help 页面](https://help.aliyun.com/product/8314910_oss.html)

-   [PostgreSQL CREATE FOREIGN TABLE 手册](https://www.postgresql.org/docs/current/sql-createforeigntable.html)

-   [OSS 错误处理](https://help.aliyun.com/document_detail/32141.html)

-   [OSS 错误响应](https://help.aliyun.com/document_detail/32005.html)


## id和key隐藏 {#section_pmk_fjg_wdb .section}

CREATE SERVER中的id和key信息如果不做任何处理，用户可以使用`select * from pg_foreign_server`看到明文信息，会暴露用户的id和key。我们通过对id和key进行对称加密实现对id和key的隐藏\(不同的实例使用不同的密钥，最大限度保护用户信息\)，但无法使用类似GP一样的方法，增加一个数据类型，会导致老实例不兼容。

最终的加密后的信息如下：

```
postgres=# select * from pg_foreign_server ;
  srvname  | srvowner | srvfdw | srvtype | srvversion | srvacl |                                                                              srvoptions
-----------+----------+--------+---------+------------+--------+------------------------------------------------------------------------------------------------------------------------------------
----------------------------------
 ossserver |       10 |  16390 |         |            |        | {host=oss-cn-hangzhou-zmf.aliyuncs.com，id=MD5xxxxxxxx，key=MD5xxxxxxxx，bucket=067862}
```

加密后的信息将会以MD5开头\(总长度为len，len%8==3\)，这样导出之后再导入不会再次加密，但是用户不能创建MD5开头的key和id。

