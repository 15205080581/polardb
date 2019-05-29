# FAQs {#concept_388449 .concept}

## Q: What is POLARDB? {#section_42u_yiy_c62 .section}

POLARDB is the next-generation relational database based on the cloud computing framework.Currently POLARDB only supports MySQL、PostgreSQL and Oracle, which is under development. The most notablefeatures are as follows:

-   Data backup time on POLARDB has been reduced to mere seconds. With the help of the excellent RDMA network and the newest block storage technology, the backup time is unrelated to the size of underlying data.
-   All of the nodes in an instance, including read/write nodes and read-only nodes, are able to access the same copy of data on a storage node. However, the traditional cloud database model only allows each instance to get its own copy of data.
-   Divide the nodes into computing nodes and storage nodes. The computing nodes are servers that primarily perform SQL parsing and storage engine computation. The storage nodes are servers that perform data block storage and data snapshots.

With these features, POLARDB satisfies both the elastic expandability needs of public cloud computing environments and the high availability needs of the database server for users on the Internet. The expansion time of read-only instances is no longer related to data size and the service can now continue even in the time between a server crash and restart.

POLARDB also features a complete management system based on Docker to handle instance creation, deletion, and account creation tasks passed down by the user. It also includes a complete and detailed monitoring system and reliable, high availability switching. The management system also maintains a set of metabases used to record the locational information of of each data block, which it provides to PolarSwitch which then passes it on to the appropriate destination. It can be said that the entire POLARDB project uses several new technologies to provide users with fast \(6x the performance of MySQL\) performance, large capacity \(up to 100 TB\), and cheap resources \(about 1/10 the cost of other commercial databases\).

## Q: When should I use POLARDB? {#section_i3s_y2l_itn .section}

-   The company has a sudden business peak
-   Data reliability requirements: RPO=0
-   Data availability requirements: RTO <60 seconds
-   Number of read-only nodes for single instance : more than 3 read-only nodes
-   Read-only node delay : Milliseconds level
-   When the enterprise uses the sharding architecture needs but have to modify the SQL
-   The enterprise must not only have the SQL versatility and reliability of the relational database, but also the scalability of NoSQL, and the multidimensional data processing convenience of the multi-mode database.
-   The enterprise has the need to replace ORACLE
-   Enterprise business need high concurrency transactions, but also need real-time complex analysis use the same database
-   The enterprise needs to retain all historical data, but has exceeded the capacity of the relational database
-   The enterprise has professional GIS, spatio-temporal data processing requirements, and the open source version can not meet the demand.

## Q: How does POLARDB work? {#section_8bg_gnd_xvt .section}

-   POLARDB is a cloud native database, computing and storage separation architecture, built-in connection proxy, automatic judgment of read and write requests, automatic distribution of read requests to read-only nodes, write requests to read-write nodes.
-   The user connects to the proxy node of the POLARDB. POLARDB is compatible with MySQL, PostgreSQL, Oracle.
-   POLARDB is compatible with MySQL, PostgreSQL, Oracle.
-   When a node abnormality occurs, failover is automatically performed, protect for zero data lost, and the impact time is less than 60 seconds.

## Q: Why is POLARDB betterthan many traditional databases? {#section_s6g_2bn_dk6 .section}

-   When upgrading hardware, you need to migrate data, the upgrade period is long, and you can't calmly respond to sudden business peaks.
-   Financial level reliability requirements RPO = 0, the traditional architecture uses the instance layer to synchronize multiple copies, performance loss.
-   The instance layer replicates the HA architecture, and the master-slave switchover time is long, which cannot meet the financial continuity business continuity requirements.
-   The traditional HA architecture adopts master-slave asynchronous replication. After the switchover, the slave library may need to be rebuilt, consumes more resources, has a long reconstruction time, and has a long-term single-point fault.
-   Each read-only node needs a copy exactly the same as the main, high cost.
-   Read and write separation using logical REDO replication, high master-slave delay.
-   Sharding architecture is not as good as imagined, functional castration, huge intrusion into the business \(restricted SQL\)
-   TB above the instance backup is slow, often dozens of hours.
-   The enterprise must not only have the SQL versatility and reliability of the relational database, but also the scalability of NoSQL, and the multidimensional data processing convenience of the multi-mode database. Traditional databases cannot be met.
-   The traditional database can not be ORACLE compatible.
-   POLARDB for Oracle is the industry's only deep Oracle-compatible database, replacing Oracle from several years to weeks.
-   POLARDB v2.0 \(for Oracle|PostgreSQL\) supports millions of QPS, 20 times performance-enhanced for complex queries, allowing enterprises to simultaneously allow OLTP+OLAP mixed load services.
-   POLARDB v2.0 \(for Oracle|PostgreSQL\) supports multi-mode capabilities, and the business can simultaneously obtain SQL versatility, NOSQL extensibility, and multi-mode development convenience.
-   POLARDB v2.0 \(for Oracle|PostgreSQL\) supports hot and cold separation, and historical data supports OSS external table storage.
-   POLARDB v2.0 \(for Oracle|PostgreSQL\) supports the GANOS professional GIS processing plug-in, which is 50 times better than the open source version.
-   POLARDB v2.0 \(for Oracle|PostgreSQL\) supports intelligent driving, SQL firewall, automatic index recommendation, performance insights, and more.

