# PolarProxy features

PolarProxy works as a proxy in a PolarDB cluster. This topic describes the following features of PolarProxy: consistency levels, transaction splitting, offloading of reads from the primary node, connection pools,parallel queries,and hints.

## PolarDB architecture and overview

![PolarDB architecture ](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2679410061/p99621.png)

PolarDB runs in a cluster architecture. Each cluster contains a primary node and one or more read-only nodes. By default, PolarDB provides two types of endpoints: primary endpoints and cluster endpoints. PolarProxy supports the cluster endpoint feature. Cluster endpoints include read/write endpoints and read-only endpoints. Read/write cluster endpoints support read/write splitting. Read-only cluster endpoints can be used to evenly distribute connections to read-only nodes. For more information about read/write splitting, see [Read/write splitting](/intl.en-US/User Guide/Connect to PolarDB/Cluster endpoint/Read/write splitting.md). The following sections describe the features of PolarProxy.

## Consistency levels

PolarDB uses asynchronous replication to synchronize data from the primary node to read-only nodes. In the read/write splitting mode, a read request that follows a write request may fail to obtain the latest write result. This issue can result in data inconsistency. PolarDB supports the following consistency levels:

-   Eventual consistency

    PolarDB synchronizes data from the primary node to read-only nodes by using asynchronous physical replication. Updates to the primary node are replicated to read-only nodes. In most cases, data changes are synchronized to read-only nodes with a latency of a few milliseconds. The latency is based on the load of write requests on the primary node. Asynchronous replication ensures eventual data consistency between the primary node and read-only nodes. This level does not guarantee data consistency when you query data through a read/write endpoint.

-   Session consistency \(recommended\)

    PolarDB uses efficient physical replication to avoid inconsistent query results caused by eventual consistency. The internal database proxy PolarProxy can be used to send read requests to read-only nodes that have updated data to achieve session consistency.

    **Note:** Session consistency ensures that the query results are consistent only within the same session. Session consistency cannot ensure the consistency between different sessions. If none of the read-only nodes meet the consistency requirement, read requests are routed to the primary node. This may result in the heavy load on the primary node.

-   Global consistency

    The read/write splitting module of PolarDB provides session consistency to ensure the causal consistency of requests within the same session. In some scenarios, logical dependencies are required both within and between sessions. For example, logical dependencies are required in scenarios when short-lived connections or connection pools are used. In this case, global consistency can be used to meet your requirements. PolarProxy tracks the replication endpoint to achieve global consistency. If a high latency exists during the replication from the primary node to read-only nodes, more requests are routed to the primary node. This increases the load on the primary node and leads to a higher service latency.


**Note:** For more information about consistency levels, see [Data consistency levels](/intl.en-US/User Guide/Connect to PolarDB/Cluster endpoint/Data consistency levels.md).

## Transaction splitting

At the default Read Committed isolation level, PolarDB does not immediately start a transaction after it receives a transactional statement. You can use BEGIN or SET AUTOCOMMIT=0 to verify that PolarDB starts the transaction after a write operation occurs.

By default, PolarProxy forwards all requests of a transaction to the primary node. However, some frameworks encapsulate all requests in the same transaction. This results in the heavy load on the primary node. To fix this issue, you can enable the transaction splitting feature. This feature allows PolarProxy to identify the current transaction status. Then, you can distribute read requests to read-only nodes by using the load balancing module before the transaction is started.

![Transaction splitting](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4528449951/p70520.png)

**Note:**

-   By default, the transaction splitting feature is enabled in the read/write splitting mode. For more information about how to modify the transaction splitting status, see [Configure transaction splitting](/intl.en-US/User Guide/Connect to PolarDB/Cluster endpoint/Read/write splitting.md).
-   The transaction splitting feature is not suitable for workloads that require global consistency. Therefore, before you enable transaction splitting, make sure that you are fully aware of the impacts of transaction splitting on your workloads.
-   The configuration takes effect only on the connections that occur after the configuration.

## Offload reads from the primary node

If you set the Offload Reads from Primary Node parameter to On for the primary node, normal read requests are no longer routed to the primary node. In transactions, read requests that require consistency are routed to the primary node to fit your needs. In addition, if all read-only nodes fail, the read requests are routed to the primary node. If your workloads do not require high consistency, you can set **Consistency Level** to **Eventual Consistency** to reduce the read requests that are routed to the primary node. You can also set the **Transaction Splitting** parameter to On to reduce the read requests that are routed to the primary node before a transaction is started. Broadcast requests, such as SET and PREPARE, are still routed to the primary node.

**Note:**

-   By default, the Offload Reads from Primary Node parameter is set to On in the read/write splitting mode.
-   Any changes to Offload Reads from Primary Node immediately take effect.

## Connection pools

PolarDB supports the following types of connection pool: session-level connection pools and transaction-level connection pools.

-   Session-level connection pool

    A session-level connection pool applies to PHP short-lived connections.

    Frequent PHP short-lived connections increase the load on a database. The session-level connection pool helps you reduce the load that is caused by frequent PHP short-lived connections. If a client is disconnected from a connection, the system determines whether the connection is idle. If the connection is idle, PolarProxy retains the connection in the connection pool for a short period. If the client sends a connection request again and the idle connection is available in the connection pool, the system assigns the idle connection to the client. The assigned connection must match the user, clientip, and dbname variables that are specified in the client request. This reduces overheads that are required to establish a new connection to a database. If no idle connections are available in the connection pool, the system establishes a new connection to the database.

    **Note:** If the session-level connection pool feature is used, the number of concurrent connections to a database is not reduced. However, the times for establishing connections between the client and the database are reduced. This helps you reduce the number of main threads that are consumed to run MySQL statements and improve service performance. However, the connections to the database include the idle connections that are retained in the connection pool.

-   Transaction-level connection pool

    A transaction-level connection pool applies to scenarios that involve a large number of connections, for example, more than 10,000 connections.

    The transaction-level connection pool is used to reduce the number of connections to the database and the load that is caused by frequent short-lived connections. A large number of connections can be established between a client and PolarProxy, but only a small number of connections can be created between PolarProxy and a database. When a client sends a connection request, PolarProxy selects an appropriate connection in the connection pool to forward the request to the database. The selected connection matches the system variables that are specified in the request. After the current transaction is terminated, PolarProxy retains the connection in the connection pool for a short period.

    A transaction connection pool has the following limits:

    -   If you perform one of the following operations, a connection is locked until the connection is closed. The locked connection is not retained in the connection pool and is unavailable to other clients.
        -   Execute the PREPARE statement.
        -   Create a temporary table.
        -   Modify user variables.
        -   Process large packets, for example, a packet of 16 MB or a larger size.
        -   Execute the LOCK TABLE statement.
        -   Execute multiple statements in a query.
        -   Call stored procedures.
    -   The FOUND\_ROWS, ROW\_COUNT, and LAST\_INSERT\_ID functions are not supported. These functions can be called, but may return invalid results.
    -   If the wait\_timeout parameter is set for a connection, the connection to the client may not time out. This is because the system assigns a connection in the connection pool to each client request. If the connection times out, the system closes only the connection between PolarProxy and the database, but retains the connection between the client and PolarProxy.
    -   The connection pool matches requests to connections by using the `sql_mode`, `character_set_server`, `collation_server`, and `time_zone` variables. If the requests include other session-level system variables, you must execute the SET statement in an explicit way to set these additional variables after the connections are established. Otherwise, the connection pool may reuse connections whose system variables have been changed.
    -   Connections may be reused. Therefore, the `SELECT CONNECTION_ID()` statement may return different thread IDs for the same connection in multiple queries.
    -   Connections may be reused. Therefore, after you execute the SHOW PROCESSLIST statement, the returned IP addresses and port numbers may be different from the actual IP addresses and port numbers of the clients.
    -   PolarProxy merges the results of the SHOW PROCESSLIST statement for all nodes and returns the results to clients. After the transaction-level connection pool is enabled, the thread ID of the connection between the client and PolarProxy is different from that between PolarProxy and the database. As a result, the KILL statement may return an error message even if the KILL statement is executed. You can execute the SHOW PROCESSLIST statement to check whether the connection is disconnected.

**Note:**

-   The configuration takes effect only on the connections that occur after the configuration.
-   If you want to enable the connection pool feature for a database account, multiple client IP addresses that are allowed to access the database cannot be granted different permissions. If you enable the connection pool feature and grant different database or table permissions to these IP addresses, a permission error may occur. For example, user@192.xx.xx.1 is granted the database\_a permission and user@192.xx.xx.2 is not granted the database\_a permission. In this case, a permission error may occur if connections to both clients are reused.
-   This connection pool feature is provided by PolarProxy and does not affect the connection pool feature of your client. If your client provides a connection pool, you do not need to enable this feature.

## Hint syntax

Add the prefix `/* FORCE_MASTER * /` or `/* FORCE_SLAVE * /` to a SQL statement to specify the direction that you want to route the SQL statement.

For example, `SELECT * FROM test` is routed to a read-only node. If the SQL statement is changed to `/* FORCE_MASTER */ SELECT * FROM test`, it is routed to the primary node.

**Note:**

-   Hints have the highest routing priority and are not constrained by the consistency level or transaction splitting. Before you use a hint, evaluate the configuration.
-   A hint cannot contain statements that change environment variables such as `/*FORCE_SLAVE*/ set names utf8;`. Otherwise, an error may occur in the subsequent procedure.

