# View cluster overview information {#concept_ych_nqr_2gb .concept}

The ApsaraDB for POLARDB console provides the cluster overview, including the following information:

-   The link topology of the cluster.
-   The CPU usage, memory usage, and connections of each node.
-   Active Thread - SQL Execution Times: includes thread running, select \(R\), insert \(R\), update \(R\), and delete \(R\). You can determine whether to display this information.
-   Slow SQL Query - Affected Rows: includes slow SQL, read \(R\), inserted \(R\), updated \(R\), and deleted \(R\). You can determine whether to display this information.
-   Lock Status: includes lock waits and lock time \(R\). You can determine whether to display this information.
-   Network Traffic: includes the input and output traffic. You can determine whether to display this information.

**Note:** In the preceding information, \(R\) indicates that the value of the field is displayed on the right Y axis.

In addition to the preceding information, the console also provides the one-click diagnosis feature for you to check the system resources, system status, session, slow SQL queries, transactions, and lock status of the node.

![](images/34793_en-US.png)

## Procedure {#section_zj3_yxk_xfb .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Find the target cluster and click the **cluster ID** in the Cluster Name column.
4.  In the left-side navigation pane, choose **Diagnostics and Optimization** \> **Cluster Overview**.
5.  Select a node in the upper-right corner and click **Diagnosis**.

    **Note:** If any issue is detected, click **View Details** to view the details.

    ![](images/34795_en-US.png)

    ![](images/34794_en-US.png)


