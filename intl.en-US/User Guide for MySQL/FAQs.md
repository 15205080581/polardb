# FAQs {#concept_266228 .concept}

## Q: Why does the database still occupy a large amount of storage after it is deleted? {#section_2ui_tcb_ywu .section}

A: This is because the redo logs occupy storage. Usually, the logs occupy around 2 to 11 GB. They can occupy up to 11 GB: 8 GB \(the 8 redo logs in the buffer pool\) + 1 GB \(the redo log being written\) + 1 GB \(the redo log created in advance\) + 1 GB \(the last redo log \).

The number of redo log files in the buffer pool is determined by the **loose\_innodb\_polar\_log\_file\_max\_reuse** parameter. The default value is 8. You can modify this parameter to reduce the storage usage of redo logs. However, when a large amount of storage is occupied, performance may fluctuate slightly in a periodic manner.

**Note:** After you modify the **loose\_innodb\_polar\_log\_file\_max\_reuse** parameter, the buffer pool will not be cleared immediately. It will be gradually released as Data Manipulation Language \(DML\) operations are performed. If you need to clear the buffer pool immediately, contact after-sales service representatives.

![loose_innodb_polar_log_file_max_reuse](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/220154/156594475647439_en-US.png)

## Q: What can I do if the disk space cannot be specified? {#section_4e1_mks_c2d .section}

A: The disk space does not need to be manually specified. The system automatically scales the space according to the data volume.

ApsaraDB for POLARDB uses a storage cluster at the underlying layer to dynamically scale up the disk space without service interruption. When the disk space usage reaches 70%, the system automatically scales up the disk space without stopping the instance. Through this mechanism, the storage space of ApsaraDB for POLARDB can be billed based on usage.

## Q: How does read-write splitting guarantee the read consistency? {#section_kkf_1k8_xff .section}

A: The read-write splitting link records the log sequence number \(LSN\). Read requests are sent to read-only nodes that meet the requirements of the LSN. For more information, see [Read-write splitting](intl.en-US/User Guide for MySQL/Read__write splitting.md#section_rfw_ys5_j2b).

## Q: How do I realize read-write splitting for ApsaraDB for POLARDB? {#section_w36_hnf_ypf .section}

A: Use cluster connection points in the application to realize read-write splitting based on the configured reader nodes. You can also use [custom cluster connection points](intl.en-US/User Guide for MySQL/Cluster and instance management/Set or release a custom cluster connection point.md#).

![Cluster connection point](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/220154/156594475648356_en-US.png)

## Q: If there are multiple read-only nodes, how do I set the specified Elastic Compute Service \(ECS\) instance to access the specified read-only nodes? {#section_592_d3f_cah .section}

A: Set a [custom cluster connection point](intl.en-US/User Guide for MySQL/Cluster and instance management/Set or release a custom cluster connection point.md#), select the read-only nodes to be connected, and then use the custom cluster connection point on the specified ECS instance.

## Q: Read-only nodes are loaded when I only use the primary endpoint. Does the primary endpoint support read-write splitting? {#section_23w_u0b_wvh .section}

A: The primary endpoint does not support read-write splitting. It is always connected to the primary node. It is normal that the query per second \(QPS\) of read-only nodes is at a low level, which is not related to the primary endpoint.

## Q: How do I find a slow SQL query? {#section_89u_bxj_qh7 .section}

A: After [Log on to POLARDB databases using DMS](../../../../intl.en-US/Quick Start for MySQL/Log on to POLARDB databases using DMS.md#), run the `show processlist;` command to find the SQL queries that have been running for a long period of time.

![Find a slow SQL query](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/220154/156594475649301_en-US.png)

## Q: How do I terminate a slow SQL query? {#section_0ne_bix_oek .section}

A: When a slow SQL query is found, view its ID and run the`kill <Id>` command to terminate the slow SQL query.

![Terminate a slow SQL query](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/220154/156594475649302_en-US.png)

