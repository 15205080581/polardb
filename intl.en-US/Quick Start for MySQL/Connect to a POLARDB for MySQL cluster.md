# Connect to a POLARDB for MySQL cluster {#task_1580301 .task}

This topic describes how to connect to a POLARDB for MySQL cluster through Data Management Service \(DMS\), through a general-purpose database client, and through the CLI.

A privileged or standard account has been created for the POLARDB cluster. For more information, see [Create accounts for a POLARDB for MySQL cluster](intl.en-US/Quick Start for MySQL/Create accounts for a POLARDB for MySQL cluster.md#).

## Connect to a POLARDB cluster through DMS {#section_wxq_bql_v2b .section}

DMS is a graphical data management tool provided by Alibaba Cloud. It offers an integrated solution for data management, structure management, access security, BI charts, data trends, data tracking, performance management, performance management. With DMS, you can manage relational databases \(including MySQL, SQL Server, and PostgreSQL\), NoSQL databases \(including MongoDB and Redis\), and Linux servers.

1.  Find the target POLARDB cluster and click its ID.
2.  In the upper-right corner, click **Log On to Database**.![基本信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3019/15665450592084_en-US.png)


3.  On the displayed logon page, enter the primary connection endpoint and port number, which are separated by a comma \(,\), enter the username and password of the privileged or standard account, and click **Log On**.![登录页面](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3019/15665450592085_en-US.png)

 

    **Note:** You can log on to your POLARDB cluster through DMS only by using the primary connection endpoint but not a cluster connection endpoint. For more information about how to view connection endpoints, see [View connection endpoints](intl.en-US/Quick Start for MySQL/View connection endpoints.md).


## Connect to a POLARDB cluster through a database client {#section_pfm_qmq_tdb .section}

You can use any general-purpose database client to connect to a POLARDB cluster. This topics uses the [HeidiSQL](https://www.heidisql.com/) database client as an example.

1.  Start HeidiSQL.
2.  In the lower-left corner, click **New**.![会话窗口](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3019/156654505954958_en-US.png)


3.  Enter the POLARDB cluster information. 

    |Parameter|Descripition|
    |---------|------------|
    |Network type|The method of connecting to the POLARDB cluster. Select **MariaDB or MySQL \(TCP/IP\)**.|
    |Hostname/IP|The private or public connection endpoint of the POLARDB cluster.     -   If the database client is deployed in an ECS instance and the region and network type of the ECS instance are the same as those of the POLARDB cluster, use the private connection endpoint to establish a secure, efficient connection.
    -   In the other situations, use the public connection endpoint.
 To view the private and public connection endpoints of the POLARDB cluster, follow these steps:     1.  Log on to the [POLARDB console](https://polardb.console.aliyun.com).
    2.  In the upper-left corner, select the region where the target POLARDB cluster is located.
    3.  Find the target POLARDB cluster and click its ID.
    4.  On the Basics page, view the private and public connection endpoints and ports.
 |
    |User|The username of the account you use to access the POLARDB cluster.|
    |Password|The password of the account you use to access the POLARDB cluster.|
    |Port|The port number corresponding to the private or public connection endpoint of the POLARDB cluster.|

4.  Click **Open**. If the connection information is correct, the POLARDB cluster gets connected.![HeidiSQL成功连接数据库](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3019/156654506055048_en-US.png)



## Connect to a POLARDB cluster through the CLI {#section_aps_qgi_pku .section}

If MySQL is installed on your server, you can run the following command to connect to a POLARDB for MySQL cluster:

``` {#codeblock_v0y_qyi_iwn}
mysql -h<Connection endpoint> -P<Port number> -u<Username> -p<Password> -D<Name of the POLARDB cluster>
```

|Parameter|Description|Example|
|---------|-----------|-------|
|-h|The private or public connection endpoint of the POLARDB cluster. For more information, see [View connection endpoints](intl.en-US/Quick Start for MySQL/View connection endpoints.md#).|`pc-bpxxxxxxxxxxxxxx.mysql.polardb.rds.aliyuncs.com`|
|-P|The port number of the POLARDB cluster. -   If you use a private connection endpoint, enter the private port number.
-   If you use a public connection endpoint, enter the public port number

 **Note:** 

-   The default port number is 3306.
-   If the default port number is used for connecting to the POLARDB cluster, you can leave this parameter blank.

 |`3306`|
|-u|The username of the account that you use to access the POLARDB cluster.|`root`|
|-p|The password of the account that you use to access the POLARDB cluster. **Note:** This parameter is optional.

-   If you do not set this parameter, the system will ask you to enter the password later.
-   If you set this parameter, do not leave any spaces between `-p` and the entered password.

 |`password233`|
|-D|The name of the POLARDB cluster to which you want to log on. **Note:** 

-   This parameter is optional.
-   You can remove `-D` and enter only the cluster name.

 |`mysql`|

![示例图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3019/156654506052711_en-US.png)

