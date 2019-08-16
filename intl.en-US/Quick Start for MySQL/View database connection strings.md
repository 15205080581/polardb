# View database connection strings {#concept_imd_wlq_tdb .concept}

Database connection strings include read/write splitting connection strings, cluster connection strings, and instance connection strings.

|Type|Description|Supported network types|Procedure|
|----|-----------|-----------------------|---------|
|Read/write splitting connection string \(recommended\)|The read/write splitting feature automatically routes requests directed at the read/write splitting connection string. It passes write requests to the primary instance and passes read requests to either the primary instance or a read-only instance based on the load of each instance.|VPC| View the connection strings on the cluster details page.

 1.  In the cluster list, find your target cluster.
2.  Click the cluster ID, or click **Manage** in the **Actions** column.
3.  View the connection strings in the **Access Information** section.

 |
|Cluster connection string|A cluster connection string always routes requests to the primary instance that enables read and write operations. If a primary instance fails, the cluster connection string will redirect the requests to a new primary instance.|VPC and public network|
|Instance connection string|An instance connection string is unique to an instance. It means that the connection string always routes requests to the instance even if the instance fails. For example, the connection string for instance A routes requests to instance A only. The same routing principle is true for instance B. If the connection string is for the primary instance, it supports both read and write operations. If the connection string is for a read-only instance, then it only supports read operations.

 |VPC and public network| View the connection strings on the instance details page.

 1.  In the instance list, find your target instance.
2.  Click the instance ID, and click **Manage** in the **Actions** column.
3.  View the connection strings in the **Access Information** section.

 |

## Network Type {#section_xxt_kpv_tdb .section}

|Network Type|Description|Application Scenario|
|------------|-----------|--------------------|
|VPC| -   This is a default connection string in the VPC. You cannot release this connection string.
-   POLARDB can achieve optimal performance when accessed in the VPC.

 | For example:

 -   An ECS instance can access databases through VPC if they are in the same VPC.
-   You can access POLARDB databases using DMS in the VPC.

 |
|Public network| -   You need to apply for a public network connection string to access POLARDB databases, and can release such connection strings.
-   The public network is the Internet. POLARDB databases cannot achieve optimal performance if it is accessed through the public network.

 |You can access and maintain your POLARDB databases through the public network.|

