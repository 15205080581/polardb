# Performance white paper {#concept_fq3_grq_tdb .concept}

This topic describes how to evaluate the optimal performance of POLARDB using Sysbench 0.5.

Sysbench is a modular, cross-platform and multi-threaded benchmark tool for evaluating important OS parameters of a system running a database under intensive load. The benchmark tool is designed to quickly evaluate the database system performance without complex database benchmark settings or even without database installations.

## Prerequisites {#section_ocn_nrq_tdb .section}

-   Three ECS instances:

-   Each instance has 32 vCPUs. For example, you can use ecs.sn1ne.8xlarge instances.
-   The ECS instances and POLARDB cluster must be in the same region and zone.
-   You must set usernames and passwords for the ECS instances.
-   The OS must be CentOS 7.4 \(64-bit\).
-   A POLARDB cluster:

-   The cluster contains one primary nodes and one read-only nodes. You must add more read-only nodes if you need to evaluate the performance of a cluster with multiple read-only inodes.
-   You must set a username and a password for the cluster.
-   You must add internal IP addresses of the ECS instances to the whitelist of your POLARDB cluster.

## Install Sysbench 0.5 {#section_w3b_lrq_tdb .section}

1.  To install Sysbench 0.5, run the following commands in ECS.

    `yum install gcc gcc-c++ autoconf automake make libtool bzr mysql-devel git mysql`

    `git clone https://github.com/akopytov/sysbench.git`

    `cd sysbench`

    `git checkout 0.5`

    `./autogen.sh`

    `./configure --prefix=/usr --mandir=/usr/share/man`

    `make`

    `make install`

2.  Run the following commands to configure the Sysbench client so that it uses all CPU cores available to process the data \(two CPU cores are used by default\), which will reduce cross-core context switching.

    `sudo sh -c 'for x in /sys/class/net/eth0/queues/rx-*; do echo ffffffff>$x/rps_cpus; done'`

    Note: ffffffff indicates 32 cores are used for data processing. Modify the command to reflect your actual configurations. For example, enter ff if your ECS instance has eight cores.

    `sudo sh -c "echo 32768 > /proc/sys/net/core/rps_sock_flow_entries"`

    `sudo sh -c "echo 4096 > /sys/class/net/eth0/queues/rx-0/rps_flow_cnt"`

    `sudo sh -c "echo 4096 > /sys/class/net/eth0/queues/rx-1/rps_flow_cnt"`


## Test procedure {#section_e3b_zxd_l2b .section}

1.  Obtain the cluster connection string and port number.
    1.  Log on to the [POLARDB console](https://polardb.console.aliyun.com/?spm=5176.2020520001.0.0.69864bd3ikTa1x#/instance/list?regionId=cn-beijing), and enter the Clusters page.
    2.  Click the cluster ID, or click **Manage** to enter the **Cluster Information** page.
    3.  Find the [View connection endpoints](../../../../intl.en-US/Quick Start for MySQL/View connection endpoints.md#) and port number.
2.  Run the following commands in ECS to create a sbtest database in the POLARDB cluster.

    `mysql -h XXX -P XXX -u XXX -p XXX -e 'create database sbtest'`

    **Note:** Replace XXX in the command and subsequent commands with your POLARDB cluster connection string \(VPC\), port number, username, and password, respectively.

3.  Preparing test data: You can create a table in the database using Sysbench, and insert data into the table.

    ``` {#codeblock_po1_zz9_v1g}
    sysbench --test=sysbench/tests/db/oltp.lua --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --mysql-table-engine=innodb --oltp-table-size=25000 --oltp-tables-count=250 --db-driver=mysql prepare
    ```

4.  Evaluate the read performance of the database using Sysbench. The evaluation will take 10 minutes.

    ``` {#codeblock_s1z_57u_n9v}
    sysbench --test=sysbench/tests/db/oltp.lua --mysql-host=XXX --oltp-tables-count=250 --mysql-user=XXX --mysql-password=XXX --mysql-port=XXX --db-driver=mysql --oltp-tablesize=25000 --mysql-db=sbtest --max-requests=0 --oltp_simple_ranges=0 --oltp-distinct-ranges=0 --oltp-sum-ranges=0 --oltp-order-ranges=0 -max-time=600 --oltp-read-only=on --num-threads=500 run
    ```

5.  Evaluate the write performance of the database using Sysbench. The evaluation will take 10 minutes.

    ``` {#codeblock_tkt_lnb_o5i}
    sysbench --test=sysbench/tests/db/oltp.lua --mysql-host=XXX --oltp-tables-count=250 --mysql-user=XXX –mysql-password=XXX --mysql-port=XXX --db-driver=mysql --oltp-tablesize=25000 --mysql-db=sbtest --max-requests=0 --max-time=600 --oltp_simple_ranges=0 --oltp-distinct-ranges=0 --oltp-sum-ranges=0 --oltporder-ranges=0 --oltp-point-selects=0 --num-threads=128 --randtype=uniform run
    ```

6.  During the tests, you can connect to the ECS instance in a new window, and run htop command to check if the CPU utilization of the Sysbench client is normal.

    `yum install htop`

    `htop`

    **Note:** 

    -   After running the htop command, you can click Q to exit.
    -   For more information about htop, go to [http://hisham.hm/htop/?spm=a2c4g.11186623.2.6.eKuBNC](http://hisham.hm/htop/).
    ![CPU使用率](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3035/15665315482111_en-US.png)

    ![CPU使用率](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3035/15665315492112_en-US.png)


## Test results {#section_lfs_dyd_l2b .section}

Obtain the QPS and TPS from the test results in the log file.

**Note:** QPS indicates the number of SQL statements \(including INSERT, SELECT, UPDATE, and DELETE\) executed by a database every second.

Test results for a single ECS instance:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3036/15665315492113_en-US.png)

Total QPS for the three ECS instances:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3036/15665315496633_en-US.png)

Total TPS for the three ECS instances:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3036/15665315506634_en-US.png)

The following figure shows the QPS for multiple read-only nodes. Five read-only nodes are used in this example, each with 4 cores and 32 GB RAM.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3036/15665315506635_en-US.png)

