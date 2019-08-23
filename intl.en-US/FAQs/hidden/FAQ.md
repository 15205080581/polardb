# FAQ {#concept_388449 .concept}

## What is ApsaraDB for POLARDB? {#section_jj0_avy_7nx .section}

ApsaraDB for POLARDB is a cloud-native relational database engine. It is compatible with the MySQL, PostgreSQL, and Oracle engines. ApsaraDB for POLARDB has been tested and practiced in the Double 11 Global Shopping Festival. ApsaraDB for POLARDB is as high-performance and secure when compared with enterprise database engines. It is also as elastic and cost-effective when compared with open-source database engines.

ApsaraDB for POLARDB is designed to handle large amounts of concurrent queries. Each cluster supports up to 100 TB of storage space and can handle up to one million queries per second \(QPS\). You can scale out a cluster to a maximum of 16 nodes. ApsaraDB for POLARDB is six times faster than traditional MySQL database engines and can help you save up to 50% of the total costs. ApsaraDB for POLARDB has high performance and high security. With ApsaraDB for POLARDB, you can scale clusters within a few minutes, recover from failures within a few seconds, and guarantee data consistency.

Since 2008, we have steadily replaced the traditional Oracle databases in the Alibaba Cloud ecosystem with ApsaraDB for POLARDB databases. ApsaraDB for POLARDB now provides substantial support for handling 98% of the transactions during the Double 11 Global Shopping Festival. During the Double 11 Global Shopping Festival in 2018, ApsaraDB for POLARDB succeeded in meeting the challenges of a transaction load that increased by 122 times in just a few seconds. From that time forward, ApsaraDB for POLARDB has been a core product of Alibaba Group.

## Why should I choose ApsaraDB for POLARDB? {#section_wgh_d24_nrv .section}

The fast development of the IT industry and Internet technologies enables enterprises and their customers to interact more frequently. The growth of interaction data is significant. Consequently, you may experience the following challenges:

-   **Storage limitations** 

    Due to the limitations of traditional MySQL databases, such as the use of physical disks and traditional data backup technology, a MySQL database cannot store data greater than 3 TB. It would be cost-prohibitive to maintain such large databases. To resolve this problem, you have to scale out clusters, migrate data, and shard databases to keep pace with the fast growth of data. This not only increases the development costs, but also causes service interruption.

-   **Scalability limitations** 

    In the traditional storage architecture, read/write and read-only nodes have their own data replicas. If you want to add a read-only node, you have to replicate all of the existing data. Due to network caps, the entire replication process can be time-consuming.

-   **Data consistency and availability limitations** 

    Traditional MySQL read/write nodes and read-only nodes use incremental synchronization to synchronize data. You have to synchronize the changes from a read/write node to a read-only node. Therefore, it takes a period of time for the data on both nodes to reach consistency. If an application retrieves data from the read-only node, the integrity of the data cannot be guaranteed. The delay issue may also adversely affect node switchover and cluster availability.


ApsaraDB for POLARDB leverages the technology that has been tested by the Double 11 Global Shopping Festival for more than 10 years. The advancement of technology allows ApsaraDB for POLARDB to adopt the elasticity of open-source database engines and the high performance of enterprise database engines with lower costs.

-   **Volumetric data storage** 

    Each ApsaraDB for POLARDB cluster supports a maximum of 100 TB of storage space and can be scaled out to up to 16 nodes. Each node can have up to 88 vCPUs. The serverless and distributed storage architecture allows you to scale clusters based on the amount of data. Fees are charged based on the actual storage usage.

-   **Extremely fast scaling against workload spikes** 

    ApsaraDB for POLARDB uses the compute and storage decoupled architecture. Compute and storage resources are independent of each other. Both compute and storage nodes are optimized to improve resource usage and performance. ApsaraDB for POLARDB is up to six times faster than traditional MySQL database engines in handling large amounts of concurrent queries. Each node can handle up to one million queries per second. It takes less than five minutes to scale out the number of compute nodes. These features enable you to handle workload spikes with ease.

-   **Data security and availability** 

    ApsaraDB for POLARDB uses one primary \(read/write\) node and multiple secondary \(read-only\) nodes. Read-only nodes and read/write nodes in a cluster share the same data replica, which greatly reduces storage costs. ApsaraDB for POLARDB also supports primary/secondary switchover with zero data loss. This resolves the issue of data inconsistency between read-only and read/write nodes caused by asynchronous replication. It takes only a few minutes to add read-only nodes, back up data, and restore data.

-   **High compatibility** 

    ApsaraDB for POLARDB is fully compatible with MySQL. You can migrate MySQL databases to the Alibaba Cloud ApsaraDB platform without modifying your code.

    ApsaraDB for POLARDB will soon release its database engines that are compatible with PostgreSQL and Oracle on the Alibaba Cloud International site.


## How ApsaraDB for POLARDB works? {#section_ulh_36o_fv5 .section}

![](images/56662_en-US.png)

ApsaraDB for POLARDB supports the following features:

-   **Compute and storage decoupling** 

    -   Compute nodes \(DB servers\): execute SQL statements, read data, and write data.
    -   Storage nodes \(data chunk servers\): store data and database snapshots. Storage nodes are grouped into clusters.
    With compute and storage decoupled, the compute resources \(CPUs and memory\) and storage resources \(disks\) no longer depend on each other. In addition, ApsaraDB for POLARDB has optimized the performance of CPUs and memory, and reduces the costs of storage. This improves resource usage and computing performance.

    Compute nodes and storage nodes are interconnected through remote direct memory access \(RDMA\) to guarantee the efficiency of data transmission.

    Unlike traditional MySQL database clusters, when you purchase an ApsaraDB for POLARDB cluster, you do not need to specify the storage space. Storage is purchased separately and billed based on your actual usage. Multiple storage plans are offered to meet your requirements. To add a read-only node, you only need to pay the computing costs. No additional storage fees are incurred.

-   **Shared storage** 

    For traditional MySQL database clusters, each node maintains a data replica. For ApsaraDB for POLARDB, all nodes in a cluster share the same replica stored on storage nodes. You do not need to replicate data when adding read-only nodes. It is fast and cost-effective to add read-only nodes. You only need to pay for the compute nodes.

-   **RDMA technology and backup optimization** 

    By leveraging the RDMA technology and Paxos block storage technology, ApsaraDB for POLARDB enables you to back up data in a few seconds. When a node fails, you can simply restart the process to resume the service.

    ApsaraDB for POLARDB supports the copy-on-write technology for you to create a snapshot in a few seconds, or create a full copy of the data in a few minutes. This technology also enables support for 100 TB disks.


**Quick migration from RDS to ApsaraDB for POLARDB**

ApsaraDB for POLARDB supports migrating RDS for MySQL 5.6 databases to ApsaraDB for POLARDB. For more information, see [../../../../dita-oss-bucket/SP\_61/DNPOLARDB19100108/EN-US\_TP\_505489.md\#](../../../../intl.en-US/Data migration__synchronization/POLARDB for MySQL/Data migration/Clone data from RDS for MySQL to POLARDB for MySQL with one click.md#).

## Why is ApsaraDB for POLARDB better than other traditional database engines? {#section_73b_04t_cl7 .section}

-   When you purchase a traditional MySQL database cluster, you must specify the size of the storage. Typically, the storage size cannot be greater than 3 TB. It may take several days to upgrade the storage space of a super large cluster. ApsaraDB for POLARDB uses storage clusters. Disks can be dynamically expanded. The disk expansion process is transparent to users and you do not need to stop the cluster during this process.
-   Traditional MySQL database engines require you to replicate data when adding read-only nodes. The scale-out speed depends on how much time the data replication takes. ApsaraDB for POLARDB allows multiple nodes to share the same storage. You can quickly add new read-only nodes without the need to replicate data.
-   Traditional MySQL read/write nodes and read-only nodes have their own data replicas. You have to pay both computing and storage costs for your purchased read-only nodes. ApsaraDB for POLARDB uses the pay-as-you-go billing method. Fees are charged based on the actual storage usage.

## How is ApsaraDB for POLARDB priced? {#section_uf5_j1h_1u1 .section}

For more information about ApsaraDB for POLARDB pricing, see [Specifications and pricing](../../../../intl.en-US/Pricing/Specifications and pricing.md#).

