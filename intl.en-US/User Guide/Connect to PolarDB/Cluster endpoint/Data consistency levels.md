# Data consistency levels

## Architecture

Apsara PolarDB runs in a cluster architecture. Each cluster contains a writer node and one or more read-only nodes. Clients can connect to an Apsara PolarDB cluster by using two types of endpoints: cluster endpoints and primary endpoints. We recommend that you use the cluster endpoints to enable access to all the nodes in the cluster and implement read/write splitting.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6159410061/p34629.png)

## Read/write splitting of PolarDB for MySQL

You can use PolarDB for MySQL to asynchronously replicate binary logs from the writer node to read-only nodes. This is a common method to replicate data and allows you to retrieve data from both the writer node and read-only nodes. This feature ensures high availability and reduces the load on the writer node.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3722729951/p34630.png)

When you use the read/write splitting feature, you must be aware of the following issues:

Clients can connect to the writer node and read-only nodes through two endpoints. You must specify the endpoint for connections. Otherwise, requests may be modified before they are forwarded to the writer node or read-only nodes.

PolarDB for MySQL implements asynchronous replication. If the system uses semi-synchronous replication, updates to the writer node cannot be synchronized in real time to all read-only nodes. Latency exists between writes and replication. Therefore, the latest updates to the writer node may not be available if you query the read-only nodes. This results in data inconsistency between the writer node and the read-only nodes.

To avoid modifications to the requests, Apsara PolarDB uses PolarProxy as a proxy to implement read/write splitting. A client connects to PolarDB for MySQL through the proxy. After a connection is established, the proxy parses each SQL request from the application and forwards requests to the database. Write requests that use the statements including UPDATE, DELETE, INSERT, and CREATE are forwarded to the writer node, and read requests that use the SELECT statement are forwarded to read-only nodes.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3722729951/p34631.png)

However, the latency between updates to the writer node and replication to read-only nodes cannot be resolved. If you execute the SELECT statement to retrieve data from the read-only nodes, the returned data may be inconsistent with the data stored on the writer node. The latency can be reduced to five seconds or fewer if the load on a MySQL cluster is low. Latency increases if the cluster processes high load in some scenarios, for example, when you execute data definition language \(DDL\) statements on a large table or insert a large amount of data to a table. You can execute DDL statements to add required columns.

## Eventual consistency, session consistency, and global consistency

-   **Eventual consistency**: Apsara PolarDB synchronizes data from the writer node to read-only nodes by using asynchronous physical replication. Updates to the writer node are replicated to read-only nodes. The latency between writes and replication depends on the load on the writer node. This asynchronous replication enables eventual consistency between the writer node and read-only nodes.
-   **Session consistency**: Data inconsistency may occur in scenarios where **eventual consistency** is used. To improve consistency and performance, Apsara PolarDB uses physical replication to synchronize data from the writer node to read-only nodes. Apsara PolarDB forwards query requests only to read-only nodes where data has been updated. For more information, see [How it works](#section_gdr_mrf_2gb).
-   **Global consistency**: In some scenarios, logical causal dependencies exist within a session or among sessions. To support the logical causal dependencies and ensure consistency among multiple sessions, **global consistency** is used in addition to **session consistency**.

## Session consistency

Apsara PolarDB runs in a read/write splitting architecture. Traditional read/write splitting ensures only eventual consistency. Latency exists between updates to the writer node and replication to read-only nodes. This may result in different responses returned by different nodes for the same query. For example, you can execute the following statements within a session:

```
INSERT INTO t1(id, price) VALUES(111, 96);
UPDATE t1 SET price = 100 WHERE id=111;
SELECT price FROM t1;
```

In this example, the result of the last query may be incorrect because Apsara PolarDB may send the SELECT request to a read-only node where data has not been updated. To solve the issue, if you use traditional database services, you must distribute requests based on workload requirements. For the workloads that require high consistency, the requests must be sent to the writer node. For the workloads that require only eventual consistency, the requests can be distributed to read-only nodes. However, this method puts a high demand on application development and increases the load on the writer node.

Apsara PolarDB provides session consistency to optimize traditional read/write splitting. Within a session, requests are sent only to read-only nodes where data has been updated.

## How it works

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3728449951/p34632.png)

Apsara PolarDB uses a proxy to achieve read/write splitting, load balancing, and read consistency. This topic describes how Apsara PolarDB achieves read consistency without increasing the load on the writer node. The proxy tracks the log sequence number \(LSN\) of the redo log for each node. When a log stored on the writer node is updated, the new LSN of the log is labeled as the session LSN. If a new read request arrives within a session, the proxy compares the session LSN and the LSN of the log stored on each node. Then, the proxy forwards the request to a read-only node where the LSN is equal to or greater than the session LSN. To enable an efficient replication, after the writer node processes a write request, the writer node returns the result to the client and replicates data to read-only nodes at the same time. Physical replication can be completed within 100 milliseconds. This allows read-only nodes to update data before subsequent read requests within the session arrive.

## Global consistency

Apsara PolarDB runs in a distributed architecture that consists of one writer node and one or more read-only nodes. Latency exists between updates to the writer node and replication to read-only nodes. This may lead to data inconsistency. For example, data may not be available in a query immediately after the data is written to the writer node. To solve this issue, Apsara PolarDB provides the read/write splitting module to enable session consistency. This feature ensures causal consistency for requests within the same session. In some scenarios, logical causal dependencies exist within a session or among sessions. To support the logical causal dependencies, global consistency is used in addition to session consistency.

![Dependencies among sessions](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3722729951/p88549.png)

In some scenarios, for example, when a connection pool is used, requests of the same thread may be sent through different connections. For the database, these requests belong to different sessions. However, logical causal dependencies exist among these requests. Global consistency is used to ensure data correctness.

**Note:** The proxy tracks the LSN of the redo log for each node to achieve global consistency. If high latency exists between updates to the writer node and replication to the read-only nodes, the number of requests forwarded to the writer node may be increased. The higher demand on the writer node may in turn prolong the latency. Global consistency is applicable to scenarios where more reads are required than writes.

## Best practices for the use of consistency levels

A higher consistency level of an Apsara PolarDB cluster indicates lower cluster performance. We recommend that you use session consistency. This consistency level makes the least changes to the cluster performance and supports most scenarios.

To enable consistency among sessions, the following solutions are available:

-   Use hints to force the writer node to run a specific query.

    ```
    eg: /*FORCE_MASTER*/ select * from user;
    ```

-   Enable global consistency.

