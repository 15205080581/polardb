# Limits

This topic describes the limits of Apsara PolarDB.

## PolarDB MySQL

|Node specification|Memory occupied by the file system|Maximum number of files|
|:-----------------|:---------------------------------|:----------------------|
|polar.mysql.x2.medium|450 MB|1,026,048|
|polar.mysql.x4.large|850 MB|2,050,048|
|polar.mysql.x4.xlarge|
|polar.mysql.x8.xlarge|
|polar.mysql.x8.2xlarge|
|polar.mysql.x8.4xlarge|
|polar.mysql.x8.12xlarge|

Description:

-   Maximum number of files

    Includes user files, database system files \(approximately 100\), and log files. To view the number of log files, run the `SHOW POLAR LOGS` command. An Apsara PolarDB table occupies two files. A partition table occupies N + 2 files, where N indicates the number of partitions. The following error message appears when you create a table after the maximum number of files is reached:

    ```
    ERROR 3017 (HY000): Too many files. PolarDB only supports 2048 files every 10GB disk size. Please drop some tables/databases before creating new tables
    ```

    In this case, you need to delete some tables or upgrade the specifications of your cluster.

-   Memory occupied by the file system

    The amount of memory that is occupied by the file system when your cluster has reached its storage limit and can read and write data normally \(neither when the cluster is under performance stress testing nor when you perform DDL operations on large tables\). The file system occupies fewer memory resources than the value specified in the table if your cluster has not reached its storage limit.


|Item|Limit|
|----|-----|
|Table name|The name of a table in a cluster of any specification must be up to 64 letters and digits or 50 Chinese characters in length.|
|Serializable isolation level|Not supported.|

