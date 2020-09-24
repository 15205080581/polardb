# Fast Query Cache

针对MySQL原生Query Cache的不足，PolarDB进行重新设计和全新实现，推出了Fast Query Cache，能够有效提高数据库查询性能。

## 前提条件

PolarDB集群版本需为PolarDB MySQL 8.0且Revision version为8.0.1.1.5或以上。

## 问题与优化

查询缓存（Query Cache）是为了提高查询性能而实现的一种缓存策略，其基本思想是：对于每个符合条件的查询语句，直接对结果集进行缓存，当下次查询命中时，直接从缓存中取出对应的结果集返回，不需要经历SQL的分析、优化、执行等复杂过程，通过节约CPU资源来达到查询加速的目标，是一项非常实用的技术。

MySQL原生Query Cache在设计和实现上存在着较多严重问题：

-   并发处理较差，在多核情况下，可能并发越高性能降低越严重。
-   内存管理较差，内存利用率低且回收不及时，造成内存浪费。
-   当缓存命中率较低时，性能无提升甚至严重降低。

由于以上问题，MySQL原生Query Cache没有得到广泛应用，在最新版的MySQL 8.0中，取消此功能。PolarDB对Query Cache进行重新设计和全新实现，进行了如下优化：

-   优化并发控制

    取消全局锁同步机制，采用无锁机制，重新设计并发场景下的同步问题，能够充分利用多核的处理能力，保证高并发场景下的性能。

-   优化内存管理

    取消内存预分配机制，采用更加灵活的动态内存分配机制，及时回收无效的内存，保证内存的真实利用率。

-   优化缓存机制

    动态检测缓存利用率，实时调整缓存策略，解决命中率偏低或读写混合等场景下的性能降低问题。


相比MySQL原生Query Cache，您可以在不同的业务场景中放心开启Fast Query Cache以提高查询性能。

## 开启Fast Query Cache

PolarDBFast Query Cache已经为不同的集群规格配置了不同的内存空间。您仅需要调整loose\_query\_cache\_type参数即可开启Fast Query Cache功能，关于如何修改参数值，请参见[设置集群参数](/intl.zh-CN/用户指南/其他操作/设置集群参数.md)。

## 性能比较

在相同场景下，分别测试QC-OFF（关闭Query Cache）和PolarDB-QC（开启Fast Query Cache）的QPS。

-   测试环境
    -   一个规格为8核64 GB的标准版PolarDB MySQL 8.0集群。
    -   Query Cache内存为4 GB。
-   测试工具

    Sysbench

-   测试数据量
    -   25张表，每张表4万条记录。
    -   25张表，每张表40万条记录。
-   测试用例

    使用以下Sysbench内置用例，分别在rand\_type=special和uniform条件下进行测试。

    -   oltp\_read\_only
    -   oltp\_point\_select
    -   oltp\_read\_write
-   测试结果及说明

    从以下测试中可以看到，Fast Query Cache在高并发场景较高命中率下性能提升非常明显。在Case1、Case3、Case4、Case5、Case6、Case7等场景中，使用了Fast Query Cache后的缓存命中率范围在63%~99%之间，最大QPS提升范围在53%~106%之间。Fast Query Cache的内存利用率很高，Case7在大数据量的point select场景中，其命中率依然达到了99%，性能提升较明显。同时在低命中率场景中，Fast Query Cache对并发性能的影响很小，基本在3%以内。对于高并发读写混合场景，性能影响也在2%以内。

    **说明：** 如下场景中的所有测试数据仅针对测试集群中的主节点。

    -   Case1：25 x 40k （tables x rows），rand-type = special oltp\_read\_only

        ![1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5841380061/p169371.png)

    -   Case2：25 x 40k （tables x rows），rand-type = uniform oltp\_read\_only

        ![2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6841380061/p169376.png)

    -   Case3：25 x 40k （tables x rows），rand-type = special oltp\_point\_select

        ![3](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6841380061/p169377.png)

    -   Case4：25 x 40k （tables x rows），rand-type = uniform oltp\_point\_select

        ![4](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5841380061/p169378.png)

    -   Case5：25 x 400k （tables x rows），rand-type = special oltp\_read\_only

        ![5](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5841380061/p169379.png)

    -   Case6：25 x 400k （tables x rows），rand-type = uniform oltp\_read\_only

        ![6](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5841380061/p169381.png)

    -   Case7：25 x 400k （tables x rows），rand-type = special oltp\_point\_select

        ![7](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5841380061/p169382.png)

    -   Case8：25 x 400k （tables x rows），rand-type = uniform oltp\_point\_select

        ![8](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5841380061/p169383.png)

    -   Case9：25 x 400k （tables x rows）， rand-type = special oltp\_read\_write

        ![9](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5841380061/p169384.png)


## 实践指南

-   适用场景指南
    -   Fast Query Cache主要目的是提高读操作性能，建议在读多写少的场景下开启，或者使用SQL\_CACHE关键字针对读多写少的表开启。如果写多读少，数据的更新非常频繁，可能会出现2%以内的性能降低。
    -   Fast Query Cache内存利用率很高，能够在更新很少但查询量很大的KV cache场景下，大幅提升数据库性能。
-   缓存使用方式（query\_cache\_type）

    Fast Query Cache完全兼容原生Query Cache的使用方法，可通过query\_cache\_type参数控制缓存。

    |参数名|取值|说明|
    |---|--|--|
    |loose\_query\_cache\_type|OFF（默认值）|禁用Fast Query Cache。|
    |ON|默认在查询中使用Fast Query Cache功能，但可通过SQL\_NO\_CACHE关键字跳过缓存。|
    |DEMAND|默认在查询中不使用Fast Query Cache功能，但可通过SQL\_CACHE关键字对特定语句使用缓存。|

    **说明：**

    loose\_query\_cache\_type参数支持会话级修改，您可以参考如下建议并根据真实业务场景进行灵活设置：

    -   对于更新频繁、写多读少等不适合Query Cache的场景，应将loose\_query\_cache\_type全局设置为OFF。
    -   对于数据量较小、访问模式比较固定、命中率较高的场景，可以将loose\_query\_cache\_type全局设置为ON。
    -   对于数据量较大、访问模式不固定、无法保障命中率的场景，可将loose\_query\_cache\_type设置为DEMAND，仅对指定的语句，通过SQL\_CACHE关键字使用Fast Query Cache。

