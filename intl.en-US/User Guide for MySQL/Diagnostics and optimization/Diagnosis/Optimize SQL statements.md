# Optimize SQL statements {#concept_l1d_pyr_2gb .concept}

The SQL optimization feature provides optimization suggestions based on the entered SQL statements. The SQL optimization feature also allows you to log on to a database and run SQL statements to insert and manage data. This topic describes how to use the SQL optimization feature to optimize and run SQL statements.

## Procedure {#section_zj3_yxk_xfb .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Find the target cluster and click the **cluster ID** in the Cluster Name column.
4.  In the left-side navigation pane, choose **Diagnostics and Optimization** \> **Diagnosis**.
5.  Click the SQL Optimization tab and click **Log On to Database** on the right.
6.  Enter the username and password, and click **Logon**.

    |Parameter|Description|
    |---------|-----------|
    |Username|The account that has the permission to manage the database.|
    |Password|The password of the account for logging on to the database.|

    ![](images/34823_en-US.png)

7.  Select the database to query or manage.

    ![](images/34824_en-US.png)

8.  Enter an SQL statement and perform the required operation.

    **Note:** All the following operations can be performed on only one SQL statement at a time. If you enter multiple SQL statements, you need to select one of them before performing subsequent operations.

    -   Click **View Execution Plan**. The detailed execution plan of the SQL statement is displayed in Execution Result.

        ![](images/34818_en-US.png)

    -   Click **Intelligent Diagnosis**. The system diagnoses the entered SQL statement and provides the optimization suggestions, such as index optimization.

        ![](images/34819_en-US.png)

    -   Click **Run Statement** and click **OK** in the dialog box that appears to run the SQL statement in the selected database. The SQL statement execution result is displayed in Execution Result.

        ![](images/34820_en-US.png)

    -   Click **Format Optimization**. The system automatically optimizes the format of the entered SQL statement.
    -   Click **Undo** to undo the modification on the SQL statement in the previous step. If you mistakenly undo the previous operation, click **Redo**. The undone modification is restored.

