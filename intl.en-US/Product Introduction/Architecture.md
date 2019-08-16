# Architecture {#concept_xqf_5ff_tdb .concept}

The architecture of the cloud-native POLARDB is shown in the following figure.

![Architecture](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3008/15659275612077_en-US.png)

## One primary instance, multiple read-only instances {#section_o1w_krf_tdb .section}

A POLARDB cluster contains one primary instance and up to 15 read-only instances \(with at least one read-only instance to provide active-active high availability support\). The primary instance processes read and write requests, while read-only instances process read requests only. POLARDB provides highly available services by performing active-active failover targeted at the primary instance or a read-only instance.

## Compute and storage separation {#section_r1f_mrf_tdb .section}

POLARDB separates compute processes from storage processes, allowing the database capacity to scale up and down to meet your application needs in Alibaba Cloud. DB servers are used only to store metadata, while data files and redo logs are stored in remote chunk servers. DB Servers only need to synchronize redo log metadata between each other, which significantly lowers the data latency between the primary instance and read-only instances. If the primary instance fails, a read-only instance can be rapidly promoted to be primary.

## Read/write splitting {#section_ycv_lcv_j2b .section}

Read/write splitting is enabled for POLARDB clusters by default, providing transparent, highly available, and self-adaptive load balancing for your database. The read/write splitting feature automatically routes requests directed at the read/write splitting connection string. It passes write requests to the primary instance and passes read requests to either the primary instance or a read-only instance based on the load of each instance. This allows the database to handle large numbers of concurrent requests.

## High speed network connection {#section_s1f_mrf_tdb .section}

To ensure strong I/O performance, high speed network connection is enabled between the DB server and the chunk server, and data are transferred using the Remote Direct Memory Access \(RDMA\) protocol.

## Shared distributed storage {#section_t1f_mrf_tdb .section}

Sharing the same group of data copies among multiple DB servers, rather than storing a separate copy of data for each DB server, significantly reduces your storage cost. The distributed storage and file system allows automatically scaling up database storage capacity, regardless of the storage capacity of each single database server. This enables your database to handle up to 100 TB of data.

## Multiple data replicas, Parallel-Raft protocol {#section_u1f_mrf_tdb .section}

Chunk servers maintain multiple data replicas to ensure reliability, and comply with the Parallel-Raft protocol to guarantee consistency among these replicas.

