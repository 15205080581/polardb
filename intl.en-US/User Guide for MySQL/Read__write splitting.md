# Read/write splitting {#concept_hbh_m45_j2b .concept}

POLARDB for MySQL clusters support read/write splitting. To enable read/write splitting, you must use the cluster address when sending requests from apps to a POLARDB for MySQL cluster. Then, the built-in proxy of the POLARDB for MySQL cluster forwards write requests to the primary node, and forwards read requests to the primary node or a read-only node based on the loads. The loads for a node is indicated by the number of requests that the node is handling.

## Benefits {#section_rfw_ys5_j2b .section}

-   **Read consistency** 

    ApsaraDB for POLARDB uses a proxy to achieve read/write splitting, load balancing, and read consistency. This topic details how ApsaraDB for POLARDB achieves read consistency without incurring much workloads for a primary node. The proxy tracks the log sequence number \(LSN\) of the redo log for each node. Each time a log stored in the primary node is updated, the new LSN of the log is labeled as the session LSN. If a new read request arrives within a session, the proxy compares the session LSN and the LSN of the log stored in each node. Then, the proxy forwards the request to a read-only node where the LSN is equal to or greater than the session LSN. To enable an instant replication, after the primary node handles a write request, it returns the result to the client and replicates data to read-only nodes at the same time. Physical replication is rapid, which allows read-only nodes to update data before subsequent read requests within the session arrive.

    ![](../DNPOLA1875676/images/34632_en-US.png)

-   **Built-in proxy for read/write splitting** 

    You can use a self-created proxy on the cloud to achieve read/write splitting. However, excessive latency may occur because data is parsed and forwarded by multiple components before arriving at a database. ApsaraDB for POLARDB uses a built-in proxy to reduce latency and enhance query performance. The proxy is deployed within the existing secure links with no additional components that consume much time in parsing and forwarding requests.

-   **O&M efficiency** 

    For traditional database services, you need to spend much effort to achieve read/write splitting. You must configure the addresses of all the primary node and read-only nodes in apps. Then, you need to distribute write requests to the primary node and read requests to read-only nodes.

    ApsaraDB for POLARDB provides an optimal solution by using a cluster address. After apps establish connections to a cluster by using the cluster address, read and write requests are automatically forwarded to the intended primary node and read-only nodes. You can view the forwarding results in the console. The cluster address minimizes your effort and cost in maintaining the ApsaraDB for POLARDB cluster.

    You can expand the capacity of an ApsaraDB for POLARDB cluster by adding read-only nodes, which alleviates your need to make any modifications for apps.

-   **Health checks for nodes** 

    ApsaraDB for POLARDB automatically performs health checks for all nodes in a cluster. If a node shuts down or has a latency that exceeds the threshold, requests will not be distributed to the node. This ensures that apps can access the ApsaraDB for POLARDB cluster even if a node crashes. After the node recovers, ApsaraDB for POLARDB automatically adds it into the list of nodes that are available to apps.

-   **Free service** 

    The read/write splitting feature is available for free.


## Forwarding logic {#section_mvw_kt5_j2b .section}

-   Forwarding logic in read/write splitting mode
    -   The following requests are forwarded to the primary node:
        -   All DML operations, such as INSERT, UPDATE, and DELETE operations
        -   All DDL operations, such as creating databases or tables, deleting databases or tables, and changing table schemas or permissions
        -   All requests in transactions
        -   Queries by using user-defined functions
        -   Queries by using stored procedures
        -   EXECUTE statements
        -   [Multi-statements](https://dev.mysql.com/doc/internals/en/multi-statement.html)
        -   Requests that involve temporary tables
        -   SELECT last\_insert\_id\(\)
        -   All requests to query or modify user environment variables
        -   SHOW PROCESSLIST statements
        -   KILL statements in SQL \(not KILL commands in Linux\)
    -   The following requests are forwarded to the primary node or read-only nodes:
        -   Non-transactional read requests
        -   COM\_STMT\_EXECUTE commands
    -   The following requests are forwarded to all nodes:
        -   All requests to modify system environment variables
        -   USE commands
        -   COM\_STMT\_PREPARE commands
        -   Commands such as COM\_CHANGE\_USER, COM\_QUIT, and COM\_SET\_OPTION
-   Forwarding logic in read-only mode:
    -   DDL and DML operations are not allowed.
    -   Requests are forwarded to read-only nodes based on load balancing.
    -   Requests cannot be forwarded to the primary node.

## Limits {#section_e1j_d55_j2b .section}

-   If you run a [multi-statement](https://dev.mysql.com/doc/internals/en/multi-statement.html) or call a stored procedure, all subsequent requests during the current session are forwarded to the primary node. To re-activate the read/write splitting feature, you must disable the current connection and establish a new connection.
-   In read-only mode, you cannot use the cluster address to configure environment variables. For example, if you run `set @endtime=now(); select * from tab where dt < @endtime`, you may not retrieve the intended environment variable.
-   When you use views, session consistency cannot be guaranteed. For example, if you run `CREATE VIEW tab2 AS SELECT * FROM tab1; INSERT INTO tab1(key, value) (1, 1); SELECT * FROM tab2 where key=1;`, the result may not be returned because of timeout.

## Apply for or modify a cluster address {#section_ksd_h55_j2b .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Find the target cluster, and click the **cluster ID** in the Cluster Name column.
4.  On the Overview page, view **Cluster Endpoints \(Recommended\)** in the Connection Information section.
5.  Click **Apply**, and in the dialog box that appears, click **Confirm**. Then, you can see the cluster address on the Overview page.

    **Note:** If an existing cluster does not have a **cluster address**, you must manually apply for the cluster address. The cluster address is automatically assigned to the new purchased cluster. If an ApsaraDB for POLARDB cluster has the cluster address, you can perform the following step to modify the address.

6.  Click **Modify**. In the Modify Endpoint dialog box, enter a new cluster address and click **Submit**.

    ![Modify a cluster address](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15443/156712814245064_en-US.png)


## FAQ {#section_hrr_m55_j2b .section}

1.  Why cannot I retrieve a newly inserted record?

    In a read/write splitting architecture, latency may occur during data replication from the primary node to read-only nodes. ApsaraDB for POLARDB ensures that the updates within a session can be retrieved.

2.  Why do read-only nodes have no workloads?

    Requests in transactions are forwarded to the primary node by default. If you use sysbench to benchmark an ApsaraDB for POLARDB cluster, you can add --oltp-skip-trx=on \(for sysbench 0.5\) or --skip-trx=on \(for sysbench 1.0\) in the code. This ensures that read requests in transactions can be forwarded to read-only nodes. If a large number of transactions incur too much workloads for the primary node, you can submit a ticket to enable distribution of transactions to read-only nodes.

3.  Why does a node receive more requests than other nodes?

    Requests are distributed to each node based on node workloads. The node that has low workloads will receive more requests.

4.  Can I retrieve the query result with no latency?

    Under common workloads, an ApsaraDB for POLARDB cluster can transmit data from the primary node to read-only nodes with a latency of milliseconds. If you want to retrieve the query result with no latency, you can use the primary address to manually send all requests to the primary node.

5.  Will new read-only nodes be automatically available to receive read requests?

    If a read-only node is added, the proxy will forward requests to the node after new connections between apps and an ApsaraDB for POLARDB cluster are established. You need to disable the current connection and establish a new connection. For example, you can restart apps.


## Related API operations {#section_06u_a6e_ibo .section}

|Operation|Description|
|:--------|:----------|
|[CreateDBEndpointAddress](../intl.en-US/API Reference/Connection points/CreateDBEndpointAddress.md#)|Creates a public network address for an ApsaraDB for POLARDB cluster.|
|[CreateDBClusterEndpoint](../intl.en-US/API Reference/Connection points/CreateDBClusterEndpoint.md#)|Creates a custom cluster address for an ApsaraDB for POLARDB cluster.|
|[DescribeDBClusterEndpoints](../intl.en-US/API Reference/Connection points/DescribeDBClusterEndpoints.md#)|Queries the address information of an ApsaraDB for POLARDB cluster.|
|[ModifyDBClusterEndpoint](../intl.en-US/API Reference/Connection points/ModifyDBClusterEndpoint.md#)|Modifies the configurations of the cluster address for an ApsaraDB for POLARDB cluster.|
|[ModifyDBEndpointAddress](../intl.en-US/API Reference/Connection points/ModifyDBEndpointAddress.md#)|Modifies the prefix of a default cluster address for an ApsaraDB for POLARDB cluster.|
|[DeleteDBEndpointAddress](../intl.en-US/API Reference/Connection points/DeleteDBEndpointAddress.md#)|Deletes the cluster address of an ApsaraDB for POLARDB cluster \(excluding the private network address\).|
|[DeleteDBClusterEndpoint](../intl.en-US/API Reference/Connection points/DeleteDBClusterEndpoint.md#)|Deletes the custom cluster address of an ApsaraDB for POLARDB cluster.|

