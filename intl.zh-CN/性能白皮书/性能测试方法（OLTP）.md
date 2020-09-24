# 性能测试方法（OLTP）

本文档介绍以SysBench工具测试PolarDB MySQL集群OLTP负载性能，您可以按照本文介绍自行测试对比，快速了解数据库系统的性能。

## 测试工具

SysBench是一个跨平台且支持多线程的模块化基准测试工具，用于评估系统在运行高负载的数据库时相关核心参数的性能表现。使用SysBench是为了绕过复杂的数据库基准设置，甚至在没有安装数据库的前提下，快速了解数据库系统的性能。

## 测试环境

-   测试的ECS和PolarDB MySQL均在同一地域、同一可用区。本例中为华东1（杭州）可用区I。
-   网络类型均为VPC网络。

    **说明：** ECS实例和PolarDB MySQL集群需保证在同一个VPC中。

-   测试用PolarDB MySQL集群如下：
    -   节点规格为polar.mysql.x4.large（4核16 GB）。
    -   只读、只写以及读写性能测试使用的是两节点集群（一主一只读）；多个只读节点性能将依次使用一主一只读到一主八只读的集群进行测试。
    -   使用的连接串为集群地址，如何查看PolarDB MySQL集群地址请参见[查看或申请连接地址](/intl.zh-CN/用户指南/集群访问/查看或申请连接地址.md)。
-   测试用ECS实例信息如下：
    -   实例规格为ecs.c5.4xlarge。
    -   实例所使用的镜像为CentOS 7.0 64位。

## 测试场景

对不同规格的PolarDB MySQL进行OLTP的只读、只写、读写以及多个只读节点的只读进行测试。

衡量指标如下：

-   TPS（Transactions Per Second）：即数据库每秒执行的事务数，以COMMIT成功次数为准。
-   QPS（Queries Per Second）：即数据库每秒执行的SQL数（含INSERT、SELECT、UPDATE、DETELE等）。

## 安装SysBench

1.  在ECS中执行如下命令安装SysBench。

    ```
    yum install gcc gcc-c++ autoconf automake make libtool bzr mysql-devel git mysql
    
    git clone https://github.com/akopytov/sysbench.git
    ##从Git中下载sysbench
    
    cd sysbench
    ##打开sysbench目录
    
    git checkout 1.0.18
    ##切换到sysbench 1.0.18版本
    
    ./autogen.sh
    ##运行autogen.sh
    
    ./configure --prefix=/usr --mandir=/usr/share/man
    
    make
    ##编译
    
    make install
    ```

2.  执行如下命令配置SysBench client，使内核可以使用所有的CPU核处理数据包（默认设置为使用2个核），同时减少CPU核之间的上下文切换。

    ```
    sudo sh -c 'for x in /sys/class/net/eth0/queues/rx-*; do echo ffffffff>$x/rps_cpus; done'
    ```

    **说明：** ffffffff表示使用32个核。请根据实际配置修改，例如ECS为8核，则输入ff。

    ```
    sudo sh -c "echo 32768 > /proc/sys/net/core/rps_sock_flow_entries"
    sudo sh -c "echo 4096 > /sys/class/net/eth0/queues/rx-0/rps_flow_cnt"
    sudo sh -c "echo 4096 > /sys/class/net/eth0/queues/rx-1/rps_flow_cnt"
    ```


## 测试方法

1.  获取PolarDB MySQL集群地址和端口。具体操作请参见[查看或申请连接地址](/intl.zh-CN/用户指南/集群访问/查看或申请连接地址.md)。

2.  关闭PolarDB MySQL集群地址的**主库不接受读**功能，具体操作请参见[修改集群地址](/intl.zh-CN/用户指南/集群访问/集群地址/修改和释放集群地址.md)。

3.  在ECS上执行如下命令，以在PolarDB MySQL集群中创建数据库testdb为例。

    ```
    mysql -h XXX -P XXX -u XXX -p XXX -e 'create database testdb'
    ```

    **说明：** 请将本命令和后续步骤的命令中的`XXX`替换为PolarDB MySQL集群的集群地址、端口号、用户名和密码，具体参数说明如下。

    |参数|说明|
    |--|--|
    |`-h`|PolarDB MySQL集群的集群地址。|
    |`-P`|PolarDB MySQL集群的端口号。|
    |`-u`|PolarDB MySQL集群的用户名。|
    |`-p`|上述用户名对应的密码。|

4.  使用SysBench测试PolarDB MySQL集群的一主节点一只读节点的只读性能，整个过程将持续10分钟。

    ```
    sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600  oltp_read_only prepare
    ##准备数据
    
    sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95 --range_selects=0 --skip-trx=1 --report-interval=1 oltp_read_only run
    ##运行workload
    
    sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95 --range_selects=0 oltp_read_only cleanup
    ##清理
    ```

5.  使用SysBench测试PolarDB MySQL集群的一主节点一只读节点的写入性能，整个过程将持续10分钟。

    ```
    sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600  oltp_write_only prepare
    ##准备数据
    
    sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95 --report-interval=1 oltp_write_only run
    ##运行workload
    
    sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95  oltp_write_only cleanup
    ##清理
    ```

6.  使用SysBench测试PolarDB MySQL集群一主节点一只读节点的混合读写性能，整个过程将持续10分钟。

    ```
    sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=250000 --tables=25 --events=0 --time=600  oltp_read_write prepare
    ##准备数据
    
    sysbench --db-driver=mysql  --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=250000 --tables=25 --events=0 --time=600   --threads=XXX --percentile=95 --report-interval=1 oltp_read_write run
    ##运行workload
    
    sysbench --db-driver=mysql  --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=250000 --tables=25 --events=0 --time=600   --threads=XXX --percentile=95  oltp_read_write cleanup
    ##清理
    ```

7.  使用SysBench测试PolarDB MySQL集群的多只读节点的只读性能（对一主节点一只读节点到一主节点八只读节点的集群依次测试）。

    ```
    sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=250000 --tables=25 --events=0 --time=600  oltp_read_only prepare
    ##准备数据
    
    sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=250000 --tables=25 --events=0 --time=600   --threads=XXX --percentile=95 --report-interval=1 oltp_read_only  --db-ps-mode=disable  --skip-trx=1  run
    ##运行workload
    
    sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=250000 --tables=25 --events=0 --time=600   --threads=XXX --percentile=95  oltp_read_only cleanup
    ##清理
    ```


-   PolarDB MySQL 8.0测试结果请参见[PolarDB MySQL 8.0性能](/intl.zh-CN/性能白皮书/PolarDB MySQL 8.0性能.md)。
-   PolarDB MySQL 5.6测试结果请参见[PolarDB MySQL 5.6性能](/intl.zh-CN/性能白皮书/PolarDB MySQL 5.6性能.md)。
-   PolarDB MySQL对比RDS MySQL测试结果请参见[与RDS MySQL的对比](/intl.zh-CN/性能白皮书/与RDS MySQL的对比.md)。

