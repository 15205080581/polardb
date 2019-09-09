# What is ApsaraDB for POLARDB? {#concept_jpz_zb2_sdb .concept}

ApsaraDB for POLARDB is a next-generation relational database service developed by Alibaba Cloud. It is compatible with MySQL, PostgreSQL, and Oracle databases. With superior performance in storage and computing, ApsaraDB for POLARDB can meet the diverse requirements of enterprises. An ApsaraDB for POLARDB cluster has a maximum storage space of 100 TB and can be configured with a maximum of 16 nodes.

ApsaraDB for POLARDB uses a storage and computing-separated architecture, in which all compute nodes share one copy of data. It can achieve vertical scaling within minutes and crash recovery within seconds. It ensures global data consistency, and offers free services for data backup and disaster recovery. ApsaraDB for POLARDB integrates the benefits of commercial databases and open source cloud databases. Commercial databases are stable, reliable, high-performance, and scalable while open source databases are easy to use and self-iterative. For example, the time a POLARDB for MySQL database takes to return results for a query reduces by five times than that a MySQL database takes. However, the cost of a POLARDB for MySQL database is only 10% that of a MySQL database.

**Cluster architecture with separate storage and computing**: ApsaraDB for POLARDB adopts a cluster architecture. Each cluster contains one read/write node \(primary node\) and multiple read-only nodes. All nodes share the data in a Polar store by using a distributed Polar file system.

**Read/write splitting**: POLARDB for MySQL uses a built-in proxy to handle external requests. When apps use a cluster address, the proxy handles all requests sent from the apps before forwarding the requests to nodes. You can use the proxy for authentication and protection and use it to achieve automatic read/write splitting. The proxy can parse SQL statements, send write requests \(such as transactions, UPDATE, INSERT, DELETE, and DDL operations\) to the primary node, and distribute read requests \(such as SELECT operations\) to multiple read-only nodes. With the proxy, apps can access POLARDB for MySQL as easily as they access a single-node MySQL database. The proxy only supports POLARDB for MySQL. We are working on support for POLARDB for PostgreSQL and POLARDB for Oracle.

## Terms {#section_y5f_gbj_5fb .section}

Familiarize yourself with the following terms to gain a better understanding of ApsaraDB for POLARDB. This helps you to find optimal purchase strategies and use the ApsaraDB for POLARDB service based on your needs.

-   Cluster: ApsaraDB for POLARDB adopts a cluster architecture. Each cluster contains one primary node and multiple read-only nodes.
-   Region: specifies the region in which a data center resides. You can achieve optimal read/write performance if ApsaraDB for POLARDB clusters and ECS instances are located in the same region.
-   Zone: A zone is a distinct location that operates on independent power grids and networks within a region. All zones in a region provide the same services.
-   Specification: specifies the resources configured for each node, such as 2 CPU cores and 4 GB.

## Benefits {#section_oq2_gbj_5fb .section}

ApsaraDB for POLARDB is compatible with MySQL, PostgreSQL, and Oracle databases. ApsaraDB for POLARDB has the following benefits:

-   **Large storage space** 

    A maximum storage space of 100 TB for an ApsaraDB for POLARDB cluster overcomes the limit of a single host and alleviates the need to purchase multiple instances for database sharding. ApsaraDB for POLARDB simplifies application development and reduces O&M workloads.

-   **Cost-effectiveness** 

    When you add a read-only node in an ApsaraDB for POLARDB cluster, you only need to pay for computing resources because of storage and computing separation. In contrast, traditional databases charge you for both computing and storage resources.

-   **Elastic scaling within minutes** 

    You can quickly scale up an ApsaraDB for POLARDB cluster because of storage and computing separation as well as shared storage.

-   **Read consistency** 

    The cluster address uses log sequence numbers \(LSNs\) to ensure global consistency in reading data and to avoid inconsistency caused by synchronization latency between the primary node and read-only nodes.

-   **Millisecond-level latency in physical replication** 

    ApsaraDB for POLARDB uses redo log-based physical replication from the primary node to read-only nodes instead of binlog-based logical replication to improve the efficiency and stability. No latency is incurred for databases even if you perform DDL operations for a large table, such as adding indexes or fields.

-   **Unlocked backup** 

    You can back up a database with a size of 2 TB within 60 seconds by using snapshots. Backup can be performed at any time on a day without any impacts on apps. During the backup process, the database will not be locked.


## Pricing {#section_ez0_hsa_fjp .section}

For more information about pricing, see [Specifications and pricing](../../../../intl.en-US/Pricing/Specifications and pricing.md#).

## Use ApsaraDB for POLARDB {#section_hwr_aoq_rgc .section}

You can use the following methods to manage ApsaraDB for POLARDB clusters, for example, to create clusters, databases, and accounts:

-   [Console](https://polardb.console.aliyun.com/): provides a visualized and easy-to-use Web interface.
-   [CLI](https://www.alibabacloud.com/help/product/29991.htm): All operations available in the console can be performed by using the command-line interface \(CLI\).
-   [SDK](../../../../intl.en-US/SDK Reference/SDK reference.md#): All operations available in the console can be performed by using the SDK.
-   [API](../../../../intl.en-US/API Reference/API overview.md#): All operations available in the console can be performed by using API operations.

After creating an ApsaraDB for POLARDB cluster, you can connect to the cluster by using the following methods:

-   DMS: You can [connect to an ApsaraDB for POLARDB cluster by using Data Management \(DMS\)](../../../../intl.en-US/Quick Start for MySQL/Connect to a POLARDB for MySQL cluster.md#section_wxq_bql_v2b) and develop databases on the Web interface.
-   Client: You can connect to an ApsaraDB for POLARDB cluster by using a database client, such as MySQL-Front and pgAdmin.

## Related services {#section_wzr_72z_tsv .section}

-   [ECS](../../../../intl.en-US/Product Introduction/What is ECS?.md): When Elastic Compute Service \(ECS\) instances access ApsaraDB for POLARDB clusters in the same region, the optimal performance of ApsaraDB for POLARDB clusters is achieved. ECS instances and ApsaraDB for POLARDB clusters compose a typical business architecture.
-   [ApsaraDB for Redis](../../../../intl.en-US/Product Introduction/What is ApsaraDB for Redis.md): ApsaraDB for Redis provides database services that use hybrid storage of memory and hard disks to ensure data consistency. You can combine ECS instances, ApsaraDB for POLARDB clusters, and ApsaraDB for Redis instances to handle a large number of read requests and reduce the response time.
-   [ApsaraDB for MongoDB](../../../../intl.en-US/Product Introduction/What is ApsaraDB for MongoDB.md): ApsaraDB for MongoDB provides a stable, reliable, and scalable database service that is compatible with the MongoDB Wire Protocol. To meet diverse business demands, you can store structured data in ApsaraDB for POLARDB and store unstructured data in ApsaraDB for MongoDB.
-   [DTS](https://www.alibabacloud.com/help/doc-detail/26592.htm): You can use Data Transmission Service \(DTS\) to migrate on-premises databases to ApsaraDB for POLARDB.
-   [OSS](../../../../intl.en-US/Product Introduction/What is OSS?.md): Object Storage Service \(OSS\) is a cloud storage service that features significant storage capacity, security, cost-effectiveness, and reliability.

