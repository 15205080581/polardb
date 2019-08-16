# Read/write splitting {#concept_hbh_m45_j2b .concept}

Read/write splitting is enabled for all POLARDB clusters by default. The system automatically assigns a read/write splitting connection string in the VPC to POLARDB clusters created after July 6, 2018. The read/write splitting feature automatically routes requests directed at the read/write splitting connection string. It passes write requests to the primary instance and passes read requests to either the primary instance or a read-only instance based on the load of each instance.

**Note:** 

-   POLARDB only offers read/write splitting connection strings in the VPC, and the service is currently unavailable in public networks.
-   You do not need to apply for a read/write splitting connection string if your cluster is created after July 6, 2018. The system automatically assigns one to all clusters created after this date. For clusters purchased before July 6, 2018, you need to apply for a read/write splitting connection string on the cluster details page.

## Benefits {#section_rfw_ys5_j2b .section}

-   **Easy to maintain** 

    Traditionally, to enable read/write splitting, you must configure connection strings of the primary instance and each read-only instance in the application, and sort out your business logic.

    In POLARDB, read/write splitting is enabled using a read/write splitting connection string that is automatically assigned to the cluster.The read/write request routing logic is transparent to you, which can lower your maintenance costs.

    You can expand processing capacity by adding read-only instances to your clusters without making any changes in the application.

-   **Improves performance with built-in read/write splitting** 

    If you construct a proxy to achieve read/write splitting, data is parsed and forwarded by multiple components before arriving at the specified database, which may impact latency. In POLARDB, the read/write splitting feature is based on a native, higly reliable link. Data does not have to pass through multiple components. This significantly lowers latency and enhances processing speed.

-   **Enhances database availability with instance health check** 

    POLARDB read/write splitting performs health checks on all instances in a cluster. When an instance fails or its latency exceeds a specified threshold, POLARDB stops routing read requests to this instance and redirect these requests to other healthy instances. The ensures that your application can still access the database if a read-only instance fails. After the instance recovers from a fault, POLARDB automatically adds the instance back to the available instance list.

-   **Reduces resource and maintenance costs with free service** 

    The read/write splitting feature is for free. You do not have to pay any additional costs.


## Routing logic {#section_mvw_kt5_j2b .section}

-   Requests sent only to the primary instance:
    -   All Data Manipulation Language \(DML\) statements \(INSERT, UPDATE, DELETE\)
    -   All Data Definition Language \(DDL\) commands \(create or remove tables and databases, modify schema, and grant permissions\)
    -   All requests in the transaction
    -   User-defined functions
    -   EXECUTE statements
    -   Requests that reference temporary tables
    -   SELECT last\_insert\_id\(\)
    -   All changes and queries made to user variables
    -   SHOW PROCESSLIST
    -   KILL \(SQL statements that contain KILL, rather than the KILL command\)
-   Requests sent to read-only instances or the primary instance
    -   Non-transactional read requests
    -   The COM\_STMT\_EXECUTE command
-   Requests always sent to all instances
    -   All modifications to system variables
    -   The USE command
    -   The COM\_STMT\_PREPARE command
    -   Commands such as COM\_CHANGE\_USER, COM\_QUIT, and COM\_SET\_OPTION

## Limits {#section_e1j_d55_j2b .section}

-   The POLARDB read/write splitting feature does not support the [COM\_PROCESS\_KILL](https://dev.mysql.com/doc/internals/en/com-process-kill.html) command, but supports SQL statements that contain KILL.
-   You must use the show processlist command to obtain the *processlist\_id* in the KILL\[CONNECTION|QUERY\]*processlist\_id* request. You cannot use the theadid/*processlist\_id* returned from the API when establishing a connection.
-   The POLARDB read/write splitting feature does not support [Multi Statements](https://dev.mysql.com/doc/internals/en/multi-statement.html) or stored procedure. If you run Multi Statements or stored procedure, all subsequent requests will be sent to the primary instance. To re-activate the read/write splitting feature, you must disconnect the current connection and reconnect to the application.

## View or modify the read/write splitting connection string {#section_ksd_h55_j2b .section}

1.  Log on to the [POLARDB console](https://polardb.console.aliyun.com/). In the left-side navigation pane, click **Clusters**.
2.  On the **Clusters** page, select a region to show all your clusters in this region.
3.  Click a cluster ID, or click **Manage** in the **Actions** column of the specified cluster.

    View or modify the read/write splitting connection string of the cluster in the Access Information section.


## FAQs {#section_hrr_m55_j2b .section}

1.  Why can't I retrieve a newly inserted record?

    A: In a read/write splitting model, the data replication from the primary instance to read-only instances may be delayed. Newly inserted records may not be retrieved immediately. Therefore, we recommend that you include operations with logic dependencies in the same transaction.

2.  Why more requests are sent to a specific instance than others?

    A: Requests are distributed according to the current load of an instance. More requests are sent to instances with low load.

3.  Does POLARDB support transferring data between the primary instance and read-only instances with zero latency?

    A: POLARDB read/write splitting connection strings do not support data transfer with zero latency. Under normal load conditions, data is transferred between the primary instance and read-only instances with milliseconds of latency. You can use a cluster connection string that routes all read/write requests to the primary instance to get rid of latency.


