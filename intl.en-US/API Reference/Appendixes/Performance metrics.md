# Performance metrics

This topic describes the performance metrics of PolarDB clusters.

## Performance metrics of PolarDB for MySQL clusters

|Performance metric|Item|Data type|Unit|Description|
|------------------|----|---------|----|-----------|
|PolarDBDiskUsage|mean\_data\_size|DOUBLE|MB|The storage space used by the data.|
|mean\_log\_size|DOUBLE|MB|The storage space used by logs.|
|mean\_sys\_dir\_size|DOUBLE|MB|The storage space used by the system.|
|mean\_tmp\_dir\_size|DOUBLE|MB|The storage space used by temporary files.|
|mean\_redolog\_size|DOUBLE|MB|The storage space used by redo logs.|
|mean\_binlog\_size|DOUBLE|MB|The storage space used by binary logs.|
|mean\_other\_log\_size|DOUBLE|MB|The size of other logs|
|mean\_undolog\_size|DOUBLE|MB|The size of undo logs.|
|PolarDBQPSTPS|mean\_qps|DOUBLE|N/A|The number of requests per second.|
|mean\_tps|DOUBLE|N/A|The number of transactions per second.|
|mean\_mps|DOUBLE|N/A|The number of operations per second.|
|PolarDBCPU|cpu\_ratio|DOUBLE|Percentage|The CPU usage.|
|PolarDBMemory|mem\_ratio|DOUBLE|Percentage|The memory usage.|
|PolarDBConnections|mean\_active\_session|DOUBLE|N/A|The number of active connections.|
|mean\_total\_session|DOUBLE|N/A|The total number of connections.|
|PolarDBNetworkTraffic|mean\_input\_traffic|DOUBLE|KB/s|The amount of inbound network traffic per second.|
|mean\_output\_traffic|DOUBLE|KB/s|The amount of outbound network traffic per second.|
|PolarDBInnoDBBufferRatio|mean\_innodb\_buffer\_dirty\_ratio|DOUBLE|Percentage|The percentage of dirty data blocks in the buffer pool.|
|mean\_innodb\_buffer\_read\_hit|DOUBLE|Percentage|The read hit ratio of the buffer pool.|
|mean\_innodb\_buffer\_use\_ratio|DOUBLE|Percentage|The utilization of the buffer pool.|
|PolarDBInnoDBDataReadWrite|mean\_innodb\_data\_read|DOUBLE|Byte|The amount of data that is read from the storage engine per second.|
|mean\_innodb\_data\_written|DOUBLE|Byte|The amount of data that is written to the storage engine per second.|
|PolarDBInnoDBBufferRequests|mean\_innodb\_buffer\_pool\_read\_requests|DOUBLE|N/A|The number of reads from the buffer pool per second.|
|mean\_innodb\_buffer\_pool\_write\_requests|DOUBLE|N/A|The number of writes to the buffer pool per second.|
|PolarDBInnoDBLogWrites|mean\_innodb\_log\_write\_requests|DOUBLE|N/A|The number of physical writes to the log file per second.|
|mean\_innodb\_os\_log\_fsyncs|DOUBLE|N/A|The number of synchronizations per second.|
|PolarDBCreatedTempDiskTable|mean\_created\_tmp\_disk\_tables|DOUBLE|N/A|The number of temporary tables created per second.|
|PolarDBCOMDML|mean\_com\_delete|DOUBLE|N/A|The number of DELETE statements executed per second.|
|mean\_com\_delete\_multi|DOUBLE|N/A|The number of Multi-DELETE statements executed per second.|
|mean\_com\_insert|DOUBLE|N/A|The number of INSERT statements executed per second.|
|mean\_com\_insert\_select|DOUBLE|N/A|The number of INSERT\_SELECT statements executed per second.|
|mean\_com\_replace|DOUBLE|N/A|The number of REPLACE statements executed per second.|
|mean\_com\_replace\_select|DOUBLE|N/A|The number of REPLACE\_SELECT statements executed per second.|
|mean\_com\_select|DOUBLE|N/A|The number of SELECT statements executed per second.|
|mean\_com\_update|DOUBLE|N/A|The number of UPDATE statements executed per second.|
|mean\_com\_update\_multi|DOUBLE|N/A|The number of Multi-UPDATE statements executed per second.|
|PolarDBRowDML|mean\_innodb\_rows\_deleted|DOUBLE|Row|The number of rows deleted per second.|
|mean\_innodb\_rows\_inserted|DOUBLE|Row|The number of rows inserted per second.|
|mean\_innodb\_rows\_read|DOUBLE|Row|The number of rows read per second.|
|mean\_innodb\_rows\_updated|DOUBLE|Row|The number of rows updated per second.|
|PolarDBIOSTAT|mean\_iops\_r|DOUBLE|N/A|The read input/output operations per second \(IOPS\).|
|mean\_iops\_w|DOUBLE|N/A|The write IOPS.|
|mean\_iops|DOUBLE|N/A|The total IOPS.|
|mean\_io\_throughput\_r|DOUBLE|MB|The read I/O throughput.|
|mean\_io\_throughput\_w|DOUBLE|MB|The write I/O throughput.|
|mean\_io\_throughput|DOUBLE|MB|The total I/O throughput.|
|PolarDBReplicaLag|mean\_replication\_delay|DOUBLE|Second|The replication delay.|

## Performance metrics of PolarDB for PostgreSQL and PolarDB-O clusters

|Performance metric|Item|Data type|Unit|Description|
|------------------|----|---------|----|-----------|
|PolarDBConnections|mean\_total\_session|DOUBLE|N/A|The total number of connections.|
|mean\_active\_session|DOUBLE|N/A|The number of active connections.|
|mean\_waiting\_connection|DOUBLE|N/A|The number of pending connections.|
|mean\_idle\_connection|DOUBLE|N/A|The number of idle connections.|
|PolarDBRowDML|mean\_tup\_returned\_delta|DOUBLE|Row|The number of rows returned per second in the full table scan result.|
|mean\_tup\_fetched\_delta|DOUBLE|Row|The number of rows returned per second in the index scan and secondary index result.|
|mean\_tup\_inserted\_delta|DOUBLE|Row|The number of rows inserted per second.|
|mean\_tup\_updated\_delta|DOUBLE|Row|The number of rows updated per second.|
|mean\_tup\_deleted\_delta|DOUBLE|Row|The number of rows deleted per second|
|PolarDBTransaction|mean\_active\_transactions|DOUBLE|N/A|The number of active transactions.|
|mean\_waiting\_transactions|DOUBLE|N/A|The number of pending transactions.|
|mean\_idle\_transactions|DOUBLE|N/A|The number of idle transactions.|
|mean\_long\_idle\_transactions|DOUBLE|N/A|The number of idle long-running transactions.|
|mean\_long\_transactions|DOUBLE|N/A|The number of long-running transactions.|
|mean\_two\_pc\_transactions|DOUBLE|N/A|The number of XA transactions.|
|mean\_long\_two\_pc\_transactions|DOUBLE|N/A|The number of long-running XA transactions.|
|PolarDBQPSTPS|mean\_tps|DOUBLE|N/A|The number of transactions per second.|
|mean\_commits\_delta|DOUBLE|N/A|The number of transactions committed per second.|
|mean\_rollbacks\_delta|DOUBLE|N/A|The number of transactions rolled back per second.|
|mean\_deadlocks\_delta|DOUBLE|N/A|The number of deadlocks per second.|
|PolarDBBuffer|mean\_blks\_read\_delta|DOUBLE|N/A|The number of block reads per second.|
|mean\_blks\_hit\_delta|DOUBLE|N/A|The number of block hits per second.|
|mean\_hit\_ratio|DOUBLE|Percentage|The block hit rate.|
|mean\_buffers\_clean|DOUBLE|N/A|The number of buffers written by the background writer during checkpoints.|
|mean\_buffers\_backend|DOUBLE|N/A|The number of buffers written by a backend.|
|mean\_buffers\_backend\_fsync|DOUBLE|N/A|The number of times that a backend was forced to execute its own fsync calls to synchronize buffers with storage.|
|mean\_buffers\_alloc|DOUBLE|N/A|The number of allocated buffers.|
|PolarDBVacuum|mean\_db\_age|DOUBLE|XID|The difference between the current transaction ID and the earliest transaction ID that cannot be reused.|
|PolarDBTemp|mean\_temp\_files|DOUBLE|N/A|The number of temporary files generated per second.|
|mean\_temp\_bytes|DOUBLE|Byte|The amount of temporary file data generated per second.|
|PolarDBCPU|cpu\_ratio|DOUBLE|Percentage|The CPU usage.|
|cpu\_user\_ratio|DOUBLE|Percentage|The CPU usage in the user mode.|
|cpu\_sys\_ratio|DOUBLE|Percentage|The CPU usage in the kernel mode.|
|PolarDBMemory|mem\_ratio|DOUBLE|Percentage|The memory usage.|
|PolarDBDiskUsage|mean\_ins\_total\_size|DOUBLE|MB|The storage space of PolarStore occupied by the cluster.|
|mean\_data\_size|DOUBLE|MB|The storage space of PolarStore occupied by user data.|
|mean\_wal\_size|DOUBLE|MB|The storage space of PolarStore occupied by Write-Ahead Logging \(WAL\) logs.|
|mean\_tmp\_size|DOUBLE|MB|The storage space occupied by temporary data.|
|mean\_log\_size|DOUBLE|MB|The storage space occupied by local logs.|
|PolarDBIOSTAT|mean\_iops\_r|DOUBLE|N/A|The read IOPS.|
|mean\_iops\_w|DOUBLE|N/A|The write IOPS.|
|mean\_iops|DOUBLE|N/A|The total IOPS.|
|mean\_io\_throughput\_r|DOUBLE|MB|The read I/O throughput.|
|mean\_io\_throughput\_w|DOUBLE|MB|The write I/O throughput.|
|mean\_io\_throughput|DOUBLE|MB|The total I/O throughput.|

