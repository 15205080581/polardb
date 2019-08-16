# Limits {#concept_tb5_rvk_xdb .concept}

## Specification limits {#section_dxq_xxk_xdb .section}

|Specifications|Memory|Memory occupied by the file system|Maximum storage|Maximum number of files|
|:-------------|:-----|:---------------------------------|:--------------|:----------------------|
|polar.mysql.x2.medium|4 GB|450 MB|5,000 GB|1,026,048|
|polar.mysql.x8.medium|16 GB|850 MB|1,000 GB|2,050,048|
|polar.mysql.x8.large|32 GB|
|polar.mysql.x8.xlarge|64 GB|
|polar.mysql.x8.2xlarge|128 GB|
|polar.mysql.x8.4xlarge|220 GB|

Note:

-   **Maximum number of files**: includes user files, database system files \(approximately 100\), and log files \(run the SHOW POLAR LOGS command to view the number of log files\). A POLARDB table occupies two files. A partition table occupies N+2 files \(N indicates the number of partitions\). The following error message will pop up if you try to create new tables after reaching the upper limit of files:

    ERROR 3017 \(HY000\): Too many files. PolarDB only supports 2048 files every 10GB disk size. Please drop some tables/databases before creating new tables

    Specifically, you must delete some tables or upgrade the specifications of your database instance.

-   **Memory occupied by the file system**: The memory occupied by the file system when your database reaches the upper limit of storage and is able to read and write normally \(that is, neither when the instance is under performance stress testing, nor when you perform DDL on large tables\). The file system occupies fewer memory resources than specified in the table if your instance has not reached its storage limit.

## Other limits {#section_a3h_syk_xdb .section}

-   **The length of table name**: The table name \(or file name\) in any database instance cannot exceed 63 English letters in length.
-   You are unable to set the serializable isolation level for your instances.
-   You cannot manage accounts in the console because your account is an advanced user by default. The permissions of POLARDB accounts are similar to those of RDS accounts for MySQL as advanced users. For more information about permissions, see [Create an account](https://help.aliyun.com/document_detail/26186.html) in ApsaraDB for RDS. 

