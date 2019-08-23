# Diagnose slow SQL queries {#concept_xc2_4qr_2gb .concept}

You can view slow Structured Query Language \(SQL\) query statistics for the databases in a cluster or on a node by date. You can also view the details of slow SQL queries for a node by time period, and view SQL recommendations and diagnostic analysis.

## Procedure {#section_f4b_sb3_mfb .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Find the target cluster and click the **cluster ID** in the Cluster Name column.
4.  In the left-side navigation pane, choose **Diagnostics and Optimization** \> **Slow SQL Query**.
5.  You can view the statistics or details of slow SQL queries as needed.
    -   Slow SQL query statistics:
        1.  Select a cluster or node in the upper-right corner. Select Slow SQL Query Statistics and specify the date and database on the left. Click **Search**.

            ![](images/34860_en-US.png)

        2.  Click an SQL statement in the SQL Statement column, and click **SQL Recommendations** to view index recommendations. You can also click **Diagnostic Analysis** to go to the [SQL Optimization](intl.en-US/User Guide for MySQL/Diagnostics and optimization/Diagnosis/Optimize SQL statements.md#) tab for diagnosis.

            ![](images/34861_en-US.png)

    -   Slow SQL query details:
        1.  Select a node in the upper-right corner. Select Slow SQL Query Details and specify the time period on the left.**** 

            **Note:** The interval between the start time and end time is 3 hours.

            ![](images/34862_en-US.png)

        2.  Click an SQL statement in the SQL Statement column, and click **SQL Recommendations** to view index recommendations. You can also click **Diagnostic Analysis** to go to the [SQL Optimization](intl.en-US/User Guide for MySQL/Diagnostics and optimization/Diagnosis/Optimize SQL statements.md#) tab for diagnosis.

