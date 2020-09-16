# Autonomy center

The diagnosis feature of PolarDB for MySQL integrates with Database Autonomy Service \(DAS\). On the Autonomy Center tab, you can enable the autonomy service. Then, if an exception occurs in a database, DAS automatically analyzes root causes, provides optimization or stop-loss suggestions, and runs optimization or stop-loss tasks. Optimization tasks are allowed based on your authorization.

## Procedure

1.  Log on to the [PolarDB console](https://polardb.console.aliyun.com/).

2.  On the top of the page, select the region where the target cluster is located.

3.  In the left-side navigation pane, click Clusters. On the **Clusters** page, click the ID of the cluster. The Overview page appears.

4.  In the left-side navigation pane, choose **Diagnostics and Optimization** \> **Diagnosis**.

5.  Click the **Autonomy Center** tab.

    ![Tab](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4687449951/p132562.png)

6.  In the upper-right corner of the tab, click **Settings**.

    ![Settings](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4687449951/p104684.png)

7.  In the **Settings** dialog box, turn on **Enable Autonomy Service**.

    **Note:** After you turn on **Enable Autonomy Service**, the system automatically performs diagnostics tests, and provides suggestions for you to optimize SQL statements.

    ![Autonomy service](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4687449951/p104686.png)

8.  Specify the following parameters: **Automatic Index Creation and Deletion**, **Automatic Throttling**, **Automatic Scale-out**, and **Automatic Scale-in**.

    -   **Automatic Index Creation and Deletion**: After you turn on **Enable Autonomy Service**, the **SQL Diagnostics** feature is automatically enabled. You can click **Enable Automatic Index Creation** to enable the system to automatically create indexes, or click **Enable Automatic Index Deletion** to enable the system to automatically delete indexes.
    -   **Automatic Throttling**: You can specify conditions to trigger automatic SQL throttling. If the specified conditions are met, automatic SQL throttling is triggered.

        **Note:** For example, automatic SQL throttling is triggered if the following conditions are met during the period specified by the Current limiting period parameter: The CPU usage is greater than 80%, the number of active sessions is greater than 64, and the duration that the situations last for is greater than 2 minutes. The Current limiting period parameter specifies the period during which SQL throttling is allowed, and the default period is from 00:00 to 23:59. The system automatically starts to check whether the conditions are met again when the automatic SQL throttling is triggered. If the problem persists, the system automatically rolls back the throttling operation. After automatic SQL throttling is triggered, the duration that the throttling operation lasts for does not exceed the value of the Maximum current limiting time parameter. For more information, see [Automatic SQL throttling](https://www.alibabacloud.com/help/zh/doc-detail/164859.htm).

    -   **Automatic Scale-out**: You can specify conditions to trigger automatic scale-out. If the specified conditions are met, scale-out is automatically triggered.

        |Parameter|Description|
        |---------|-----------|
        |**Average CPU utilization**|The threshold to trigger automatic scale-out. If the **average CPU usage** is greater than or equal to the specified value, automatic scale-out is triggered.|
        |**Maximum Specifications**|The maximum value to which the cluster specification can be automatically scaled out. After automatic scale-out is triggered, the system scales out PolarDB cluster specifications to the maximum specification level by level. For example, the system scales out cluster specifications from four cores to eight cores, and then to 16 cores.**Note:**

        -   Cluster specification scale-out does not affect existing data in clusters.
        -   When the system scales cluster specifications, PolarDB clusters may experience transient connection errors for a few seconds and some operations are unavailable. Make sure that your application can automatically connect to PolarDB for MySQL clusters. |
        |**Maximum number of read-only nodes**|The maximum number of read-only nodes that can be automatically added to the cluster. After automatic scale-out is triggered, the read-only nodes of PolarDB are added one after one until the upper limit is reached.|
        |**Observation Window**|DAS checks whether the conditions to trigger automatic scale-out or scale-in are met in a periodical manner. If the CPU usage reaches the specified value for more than 50% of the duration of an observation window, DAS triggers automatic scale-out when the observation window ends. By default, if the CPU usage is greater than 70% for more than 50% of the duration of an observation window, DAS triggers automatic scale-out when the observation window ends.|
        |**Quiescent Period**|The minimum interval between two automatic scale-in or scale-out operations. During a quiescent period, DAS continues checking whether the conditions to trigger automatic scale-out or scale-in are met. However, during the quiescent period, DAS cannot trigger automatic scale-out or scale-in even if the specified conditions are met. A quiescent period and an observation window may end at the same time. In this case, if the specified conditions are met within the observation window, DAS triggers automatic scale-out or scale-in when the quiescent period and the observation window end.|

    -   **Automatic Scale-in**: After you enable the feature, if the CPU usage is less than 30% for more than 99% of the duration of an observation window, DAS triggers automatic scale-in. The system scales in PolarDB cluster specifications to the original specifications level by level.
9.  Click **Determine**.


