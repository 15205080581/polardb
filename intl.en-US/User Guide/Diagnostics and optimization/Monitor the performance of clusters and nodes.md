# Monitor the performance of clusters and nodes

The PolarDB console provides a variety of performance metrics, and allows you to collect monitoring data at intervals of a few seconds. This helps you monitor the status of your clusters, and locate faults by using the monitoring data that is collected in a fine-grained manner.

## Monitor the performance of clusters and nodes

1.  Log on to the [PolarDB console](https://polardb.console.aliyun.com/).

2.  On the top of the page, select the region where the target cluster is located.

3.  Find the target cluster and click the cluster ID to go to the Overview page.

4.  In the left-side navigation pane, choose **Diagnostics and Optimization** \> **Monitoring**.

5.  You can view the monitoring information about a **Cluster** or **Node** based on your business requirements. For more information, see [Metric description](#section_ab1_kij_u21).

    -   To monitor cluster performance, click the **Cluster** tab. Specify a monitoring period in the date and time picker and click **OK**.

        ![Cluster performance monitoring](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0232729951/p34680.png)

    -   To monitor node performance, click the **Node** tab and select a node from the drop-down list. Specify a monitoring period in the date and time picker and click **OK**.

        ![Node performance monitoring](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0232729951/p34681.png)


**Note:** On the [Real-time Monitoring Dashboard](https://hdm.console.aliyun.com/#/dashboard/convoy) page in the Database Autonomy Service \(DAS\) console, you can view the monitoring data of PolarDB for MySQL. This helps you identify abnormal clusters for further analysis and optimization.

## Metric description

|Category|Metrics|Description|
|--------|-------|-----------|
|Cluster|Storage|Displays the sizes of binary log files, redo log files, and other log files, as well as the usage of data storage, system storage, and temporary storage.|
|QPS|Displays the queries per second \(QPS\) of each node.|
|TPS|Displays the transactions per second \(TPS\) of each node.|
|MPS|Displays the manipulations per second \(MPS\) of each node.|
|CPU|Displays the CPU usage of each node.|
|Memory Usage|Displays the memory usage of each node.|
|Node|QPS|Displays the QPS of the selected node.|
|TPS|Displays the TPS of the selected node.|
|MPS|Displays the MPS of the selected node.|
|CPU|Displays the CPU usage of the selected node.|
|Memory Usage|Displays the memory usage of the selected node.|
|Connections|Displays the total number of connections and the number of active connections on the selected node.|
|Operations|Displays the number of operations per second performed on the selected node, including the DELETE, INSERT, UPDATE, and REPLACE operations.|
|Memory Buffer Pool|Displays the dirty ratio, read hit ratio, and usage of the buffer pool on the selected node.|
|I/O Throughput|Displays the total I/O throughput, I/O read throughput, and I/O write throughput of the selected node.|
|IOPS|Displays the input/output operations per second \(IOPS\) of the selected node, including the total IOPS, the read IOPS, and the write IOPS.|
|Network|Displays the input and output traffic per second of the selected node.|
|Scanned Rows|Displays the numbers of rows that are inserted, read, updated, and deleted per second on the selected node.|
|InnoDB Read and Written Data|Displays the amount of data that is read from or written into the storage engine per second on the selected node.|
|InnoDB Buffer Pool Requests|Displays the number of read and write operations that are performed on the buffer pool of the selected node per second.|
|InnoDB Log Writes|Displays the number of log write requests per second and the number of data synchronizations to disks per second on the selected node.|
|Temporary Tables|Displays the number of temporary tables that are created per second on the selected node.|

## Change data collection intervals

1.  Log on to the [PolarDB console](https://polardb.console.aliyun.com/).

2.  On the top of the page, select the region where the target cluster is located.

3.  Find the target cluster and click the cluster ID to go to the Overview page.

4.  In the left-side navigation pane, choose **Diagnostics and Optimization** \> **Monitoring**.

5.  Click **Change Data Collection Interval**.

    ![Change the data collection interval - 1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3953320061/p95368.png)

6.  In the **Change Data Collection Interval** dialog box, set **Data Collection Interval** to **5s** or **60s** based on your business requirements. The default value is 60s.

    ![Change the data collection interval](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/3953320061/p95366.png)

    -   Scenarios where the **Data Collection Interval** parameter is set to **5s**
        -   If the query time range is less than or equal to 1 hour, the monitoring data is displayed at intervals of 5 seconds.
        -   If the query time range is less than or equal to one day, the monitoring data is displayed at intervals of 1 minute.
        -   If the query time range is less than or equal to seven days, the monitoring data is displayed at intervals of 10 minutes.
        -   If the query time range is less than or equal to 30 days, the monitoring data is displayed at intervals of 1 hour.
        -   If the query time range is greater than 30 days, the monitoring data is displayed at intervals of one day.
    -   Scenarios where the **Data Collection Interval** parameter is set to **60s**
        -   If the query time range is less than or equal to one day, the monitoring data is displayed at intervals of 1 minute.
        -   If the query time range is less than or equal to seven days, the monitoring data is displayed at intervals of 10 minutes.
        -   If the query time range is less than or equal to 30 days, the monitoring data is displayed at intervals of 1 hour.
        -   If the query time range is greater than 30 days, the monitoring data is displayed at intervals of one day.
7.  Click **OK**.


## Related operations

|API|Description|
|---|-----------|
|[DescribeDBClusterPerformance](/intl.en-US/API Reference/Monitoring management/DescribeDBClusterPerformance.md)|Queries the performance data of a PolarDB cluster.|
|[DescribeDBNodePerformance](/intl.en-US/API Reference/Monitoring management/DescribeDBNodePerformance.md)|Queries the performance data of the nodes in a PolarDB cluster.|
|[DescribeDBClusterMonitor](/intl.en-US/API Reference/Monitoring management/DescribeDBClusterMonitor.md)|Queries the interval for collecting the monitoring data of a PolarDB cluster.|
|[ModifyDBClusterMonitor](/intl.en-US/API Reference/Monitoring management/ModifyDBClusterMonitor.md)|Changes the interval for collecting the monitoring data of a PolarDB cluster.|

