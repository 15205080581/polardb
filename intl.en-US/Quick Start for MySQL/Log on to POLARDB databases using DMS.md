# Log on to POLARDB databases using DMS {#concept_n2f_4mq_tdb .concept}

[Data Management Service \(DMS\)](https://account.aliyun.com/login/login.htm?oauth_callback=https%3A%2F%2Fdms-rds.aliyun.com) is a cloud-based, all-in-one solution that supports cluster data management, schema management, access control, Business Intelligence \(BI\) system, data trends, data tracking, database performance tune-up, and server management. You can use DMS to manage relational databases such as MySQL, SQL Server and PostgreSQL, NoSQL databases \(including MongoDB and Redis\), as well as Linux servers.

## Prerequisites {#section_ofm_qmq_tdb .section}

You must create an initial account or a classic user for your POLARDB cluster. For more information about how to create an initial account, see [Create an initial account for a POLARDB cluster](https://help.aliyun.com/document_detail/68508.html).

## Procedure {#section_pfm_qmq_tdb .section}

1.  Enter cluster list or instance list, and find your target cluster or instance.
2.  Click the cluster ID or instance ID, or click **Manage** in the **Actions** column.
3.  Click **Log On Database** in the upper-right corner of the page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3019/15659359382084_en-US.png)

4.  On the database logon page, enter the connection string for accessing POLARDB databases in a VPC network and the port number, and separate them with a colon \(:\). Then enter the username and the password of the initial account or the classic users, and click **Log On**.

    -   If you enter the database logon page redirected from the cluster details page, the system will automatically enter the connection string and port number of the corresponding cluster in VPC.

    -   If you enter the database logon page redirected from the instance details page, the system will automatically enter the connection string and port number of the corresponding instance in VPC.

    For more information about how to view the connection strings and port number, see [View database connection strings](https://help.aliyun.com/document_detail/68510.html).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3019/15659359382085_en-US.png)


**Note:** If you want your browser to remember your account password, you can select **Remember Password** before clicking **Log On**.

