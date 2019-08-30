# Performance monitoring and alert configuration {#concept_gwv_lqq_tdb .concept}

The ApsaraDB for POLARDB console provides a variety of performance metrics for you to monitor the status of your instances.

## Monitor performance {#section_fr1_qqq_tdb .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Find the target cluster and click the **cluster ID** in the **Cluster Name** column.
4.  In the left-side navigation pane, choose **Diagnostics and Optimization** \> **Monitoring**.
5.  You can view the performance information of a **cluster** or **node** according to your needs. For more information, see [Metric description](#).
    -   To monitor cluster performance, click the **Cluster** tab and set the monitoring time period.****

        ![Cluster performance monitoring](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3031/156715767834680_en-US.png)

    -   To monitor node performance, click the **Node** tab, select a node, and set the monitoring time period.**** 

        **Note:** You can click **More** at the bottom of the Node tab to view more metrics.

        ![Node performance monitoring](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3031/156715767834681_en-US.png)

        ![Node performance monitoring](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3031/156715767834796_en-US.png)


## Metric description {#section_ab1_kij_u21 .section}

|Type|Metric|Description|
|----|------|-----------|
|Cluster|Storage|Displays the size of log files such as binlog and redolog, as well as the usage of data storage, system storage, and temporary storage.|
|QPS|Displays the queries per second \(QPS\) of each node.|
|TPS|Displays the transactions per second \(TPS\) of each node.|
|CPU|Displays the central processing unit \(CPU\) usage of each node.|
|Memory|Displays the memory usage of each node.|
|Node|QPS|Displays the QPS of the selected node.|
|TPS|Displays the TPS of the selected node.|
|CPU|Displays the CPU usage of the selected node.|
|Memory|Displays the memory usage of the selected node.|
|Connections|Displays the total number of connections and the number of active connections on the selected node.|
|Operations|Displays the number of operations performed on the selected node per second, including the DELETE, INSERT, UPDATE, and REPLACE operations.|
|Memory Buffer Pool|Displays the dirty ratio, read hit ratio, and usage of the buffer pool on the selected node.|
|I/O Throughput|Displays the total I/O throughput, I/O read throughput, and I/O write throughput of the selected node.|
|IOPS|Displays the input/output operations per second \(IOPS\) of the selected node, including the total IOPS, read IOPS, and write IOPS.|
|Network|Displays the input and output traffic per second of the selected node.|
|Scanned Rows|Displays the numbers of rows inserted, read, updated, and deleted per second on the selected node.|
|InnoDB Read and Written Data|Displays the amount of data read from or written into the storage engine per second on the selected node.|
|InnoDB Buffer Pool Requests|Displays the numbers of read and write operations performed on the buffer pool of the selected node per second.|
|InnoDB Log Writes|Displays the number of log write requests per second and the number of times that data is synchronized to disks per second on the selected node.|
|Temporary Table|Displays the number of temporary tables created per second on the selected node.|

## Configure alert rules {#section_ugr_15h_1gb .section}

1.  Log on to the [CloudMonitor console](https://cms-intl.console.aliyun.com).
2.  In the left-side navigation pane, choose **Alarms** \> **Alarm Rules**.
3.  On the Alarm Rules page, click **Create Alarm Rule**.

    ![Create alert rules](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3031/156715767853821_en-US.png)

    **Note:** For more information about alert rules, see [Alarm rule parameters](../../../../intl.en-US/User Guide/Alarm service/Alarm rules/Alarm rule parameters.md#).

4.  Select relevant resources, set alert rules and the notification method, and click **Confirm**.

