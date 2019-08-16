# Benefits {#concept_dpc_ytf_tdb .concept}

## Easy to use {#section_ipv_tvf_tdb .section}

POLARDB is fully compatible with MySQL, which means that the code, applications, and drivers you use with your existing MySQL databases can be used with POLARDB with little or no changes required.

## High performance {#section_ryk_4qv_tdb .section}

-   The POLARDB architecture improves on the MySQL kernel, and adopts physical replication, RDMA protocol, and shared distributed storage, improving the read performance up to six times when compared to MySQL.

-   A POLARDB cluster contains one primary instance and up to 15 read-only instances \(with at least one read-only instance acting to provide active-active high availability solutions\) so that you can perform concurrent read and write operations.


## Massive storage {#section_kpv_tvf_tdb .section}

Distributed block storage and file system is used in the POLARDB architecture to support a capacity of up to 100 TB per database instance.

## High availability {#section_lpv_tvf_tdb .section}

POLARDB performs automated failovers targeted at the primary instance, or a read-only instance, by using an active-active high availability architecture. This architecture brings better system access performance than a traditional active-standby setup at the same cost.

## Data security and reliability {#section_mpv_tvf_tdb .section}

POLARDB provides various security measures for your database access, storage, and management. These include managing data access by whitelisting IP addresses, network isolation using Virtual Private Cloud \(VPC\), encryption of data in transit using SSL, and storage of data in multiple copies.

## Low cost {#section_npv_tvf_tdb .section}

POLARDB lowers storage costs by applying a shared storage mechanism.

## Scalability and expandability {#section_opv_tvf_tdb .section}

POLARDB enables easy CPU and memory expansion by using container virtualization and shared distributed block storage technology. It takes only 2-3 minutes to add a secondary instance to your database. Based on your database usage, the database storage will automatically scale towards the upper limit of your storage \(depending on the specifications of your instance\), with no impact on business continuity.

