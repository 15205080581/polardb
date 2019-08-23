# 什么是POLARDB {#concept_jpz_zb2_sdb .concept}

POLARDB是阿里云自研的下一代关系型云数据库，兼容MySQL、PostgreSQL、Oracle引擎，存储容量最高可达100TB，单库最多可扩展到16个节点，适用于企业多样化的数据库应用场景。

POLARDB采用存储和计算分离的架构，所有计算节点共享一份数据，提供分钟级的配置升降级、秒级的故障恢复、全局数据一致性和免费的数据备份容灾服务。POLARDB既融合了商业数据库稳定可靠、高性能、可扩展的特征，又具有开源云数据库简单开放、自我迭代的优势，例如POLARDB for MySQL性能最高可以提升至MySQL的6倍，而成本只有商用数据库的1/10。

**集群架构，计算与存储分离：**POLARDB采用多节点集群的架构，集群中有一个Writer节点（主节点）和多个Reader节点（读节点），各节点通过分布式文件系统（PolarFileSystem）共享底层的存储（PolarStore）。

**读写分离**：当应用程序使用集群地址时，POLARDB for MySQL通过内部的代理层（Proxy）对外提供服务，应用程序的请求都先经过代理，然后才访问到数据库节点。代理层不仅可以做安全认证和保护，还可以解析SQL，把写操作（比如事务、UPDATE、INSERT、DELETE、DDL等）发送到主节点，把读操作（比如SELECT）均衡地分发到多个只读节点，实现自动的读写分离。对于应用程序来说，就像使用一个单点的MySQL数据库一样简单。内部的代理层（Proxy）后续将支持POLARDB for PostgreSQL/Oracle。

## 相关概念 {#section_y5f_gbj_5fb .section}

了解以下概念，将帮助您更好地选购和使用POLARDB：

-   集群：POLARDB采用集群架构，一个集群包含一个主节点和多个读节点。
-   地域：地域是指物理的数据中心。一般情况下，POLARDB集群应该和ECS实例位于同一地域，以实现最高的访问性能。
-   可用区：可用区是指在某个地域内拥有独立电力和网络的物理区域。同一地域的不同可用区之间没有实质性区别。
-   规格：每个节点的资源配置，比如2核4GB。

## 产品优势 {#section_oq2_gbj_5fb .section}

您可以像使用MySQL、PostgreSQL、Oracle一样使用POLARDB，此外，POLARDB还有传统数据库不具备的优势：

-   **容量大** 

    最高100TB，您不再需要因为单机容量的天花板而去购买多个实例做分片，由此简化应用开发，降低运维负担。

-   **高性价比** 

    POLARDB的计算与存储分离，每增加一个只读节点只收取计算资源的费用，而传统的只读节点同时包含计算和存储资源，每增加一个只读节点需要支付相应的存储费用。

-   **分钟级弹性** 

    存储与计算分离的架构，配合共享存储，使得快速升级成为现实。

-   **读一致性** 

    集群地址利用LSN（Log Sequence Number）确保读取数据时的全局一致性，避免因为主备延迟引起的不一致。

-   **毫秒级延迟（物理复制）** 

    利用基于Redo的物理复制代替基于Binlog的逻辑复制，提升主备复制的效率和稳定性。即使对大表进行加索引、加字段等DDL操作，也不会造成数据库的延迟。

-   **无锁备份** 

    利用存储层的快照，可以在60秒内完成对2TB数据量大小的数据库的备份，而且备份过程不会对数据库加锁，对应用程序几乎无影响，全天24小时均可进行备份。


## 相关服务 {#section_dru_7os_cmo .section}

-   [ECS](../../../../intl.zh-CN/产品简介/什么是云服务器ECS.md)：ECS是云服务器，通过内网访问同一地域的POLARDB集群时，可实现POLARDB集群的最佳性能。ECS搭配POLARDB集群是典型的业务访问架构。
-   [Redis](../../../../intl.zh-CN/产品简介/什么是云数据库Redis版.md)：Redis提供持久化的内存数据库服务。当业务访问量较大时，ECS 、POLARDB和Redis的组合可以支持更多的读请求，同时减少响应时间。
-   [MongoDB](../../../../intl.zh-CN/产品简介/什么是云数据库MongoDB版.md)：提供稳定可靠、弹性伸缩、完全兼容MongoDB协议的数据库服务。数据结构多样时，可以选择将结构化数据存储在POLARDB，将非结构化数据存储在MongoDB，满足业务的多样化存储需求。
-   [DTS](https://help.aliyun.com/document_detail/26592.html)：您可以使用数据传输服务DTS将本地数据库迁移到云上的POLARDB。
-   [OSS](../../../../intl.zh-CN/产品简介/什么是对象存储 OSS.md)：对象存储服务OSS是阿里云提供的海量、安全、低成本、高可靠的云存储服务。

## 如何使用POLARDB {#section_hwr_aoq_rgc .section}

您可以通过以下方式管理POLARDB集群，进行集群创建、数据库创建、账号创建等操作：

-   [控制台](https://polardb.console.aliyun.com/)：提供图形化的Web界面，操作方便。
-   [CLI](https://help.aliyun.com/product/29991.html)：控制台上所有的操作都可以通过CLI实现。
-   [SDK](../../../../intl.zh-CN/SDK参考/SDK参考.md#)：控制台上所有的操作都可以通过SDK实现。
-   [API](../../../../intl.zh-CN/API参考/API概览.md#)：控制台上所有的操作都可以通过API实现。

创建POLARDB集群后，您可以通过以下方式连接POLARDB集群：

-   DMS：您可以[通过DMS连接POLARDB集群](../../../../intl.zh-CN/POLARDB for MySQL快速入门/连接数据库集群.md#section_wxq_bql_v2b)，在Web界面进行数据库开发工作。
-   客户端：您可以使用通用的数据库客户端工具连接POLARDB集群。例如，MySQL-Front、pgAdmin等。

## POLARDB定价 {#section_edl_vs8_qbv .section}

详情请参见[规格与定价](../../../../intl.zh-CN/产品定价/规格与定价.md#)。

