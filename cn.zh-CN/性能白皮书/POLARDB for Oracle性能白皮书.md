# POLARDB for Oracle性能白皮书 {#concept_221615 .concept}

本文档介绍如何使用pgbench测试POLARDB for Oracle集群主节点的最大性能。

PostgreSQL自带一款轻量级的压力测试工具pgbench。pgbench是一种在PostgreSQL（兼容Oracle）上运行基准测试的简单程序，它可以在并发的数据库会话中重复运行相同的SQL命令。

## 测试环境 {#section_ocn_nrq_tdb .section}

-   所有测试均在本地测试完成（使用IP+端口）。
-   ECS的实例规格：ecs.g5.16xlarge（64核 256GiB）
-   网络类型：专有网络
-   操作系统：CentOS 7.6 x64

    **说明：** CentOS 6不支持PostgreSQL 11。


## 测试指标 {#section_4c2_yrq_0z3 .section}

-   **只读QPS** 

    数据库只读时每秒执行的SQL数（仅包含SELECT）。

-   **读写QPS** 

    数据库读写时每秒执行的SQL数（包含INSERT、SELECT、UPDATE）。


## 准备工作 {#section_w3b_lrq_tdb .section}

-   **安装测试工具** 

    执行如下命令在ECS实例中安装PostgreSQL 11。

    ``` {#codeblock_d3j_k8t_v15}
    yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
    yum install -y https://download.postgresql.org/pub/repos/yum/11/redhat/rhel-7-x86_64/pgdg-centos11-11-2.noarch.rpm
    yum install -y postgresql11*
    su - postgres
    vi .bash_profile
    export PS1="$USER@`/bin/hostname -s`-> "    
    export LANG=en_US.utf8    
    export PGHOME=/usr/pgsql-11  
    export LD_LIBRARY_PATH=$PGHOME/lib:/lib64:/usr/lib64:/usr/local/lib64:/lib:/usr/lib:/usr/local/lib:$LD_LIBRARY_PATH    
    export DATE=`date +"%Y%m%d%H%M"`  
    export PATH=$PGHOME/bin:$PATH:.    
    export MANPATH=$PGHOME/share/man:$MANPATH    
    alias rm='rm -i'    
    alias ll='ls -lh'    
    unalias vi
    ```

-   **修改Oracle集群参数** 

    由于部分参数无法在控制台直接修改，您需要提交工单申请，修改POLARDB for Oracle集群的yaml配置文件如下：

    ``` {#codeblock_rfp_hmy_0h9}
    default_statistics_target: "100"
    max_wal_size: "64GB" #half mem size
    effective_cache_size: "96GB" #3/4 mem size
    max_parallel_workers_per_gather: "16" #half cpu core number
    maintenance_work_mem: "2GB" #1/32 mem, don't exceed 8GB
    checkpoint_completion_target: "0.9"
    max_parallel_workers: "32" #cpu core number,don't exceed 64
    max_prepared_transactions: "2100"
    archive_mode: "off"
    work_mem: "64MB" #mem 1/2000,don't exceed 128MB
    wal_buffers: "16MB"
    min_wal_size: "64GB" #1/4 mem size, min size 3GB (3 wal files, 2 as preallocated)
    shared_buffers: "192GB" #75% mem size 8GB
    max_connections: "12900"
    polar_bulk_extend_size: "4MB"
    polar_xlog_record_buffers: "25GB" #10~15% mem size,min size 1GB
    hot_standby_feedback: "on"
    full_page_writes: "off"
    synchronous_commit: "on"
    polar_enable_async_pwrite: "off"
    polar_parallel_bgwriter_delay: "10ms"
    polar_max_non_super_conns: '12800'
    polar_parallel_new_bgwriter_threshold_lag: "6GB"
    polar_use_statistical_relpages: "on"
    polar_vfs.enable_file_size_cache: "on"
    ```

    **说明：** 以规格为polar.o.x8.4xlarge（32核 256GB）的集群为例修改配置文件，同时为了和RDS对比，修改内存和RDS for PostgreSQL相同。

    修改配置后，重启Oracle集群让配置生效。


## 测试方法 {#section_e3b_zxd_l2b .section}

1.  根据目标库大小初始化测试数据，具体命令如下：
    -   初始化数据50亿：`pgbench -i -s 50000`
    -   初始化数据10亿：`pgbench -i -s 10000`
    -   初始化数据5亿：`pgbench -i -s 5000`
    -   初始化数据1亿：`pgbench -i -s 1000`
2.  通过以下命令配置环境变量：

    ``` {#codeblock_5ry_sf5_tmr}
    export PGHOST=<Oracle集群主节点私网地址>
    export PGPORT=<Oracle集群主节点私网端口>
    export PGDATABASE=postgres
    export PGUSER=<Oracle数据库用户名>
    export PGPASSWORD=<Oracle对应用户的密码>
    ```

3.  创建只读和读写的测试脚本。
    -   创建只读脚本ro.sql内容如下：

        ``` {#codeblock_jgy_91a_k0x}
        \set aid random_gaussian(1, :range, 10.0)
        SELECT abalance FROM pgbench_accounts WHERE aid = :aid;
        ```

    -   创建读写脚本rw.sql内容如下：

        ``` {#codeblock_pq1_cro_38s}
        \set aid random_gaussian(1, :range, 10.0)
        \set bid random(1, 1 * :scale)
        \set tid random(1, 10 * :scale)
        \set delta random(-5000, 5000)
        BEGIN;
        UPDATE pgbench_accounts SET abalance = abalance + :delta WHERE aid = :aid;
        SELECT abalance FROM pgbench_accounts WHERE aid = :aid;
        UPDATE pgbench_tellers SET tbalance = tbalance + :delta WHERE tid = :tid;
        UPDATE pgbench_branches SET bbalance = bbalance + :delta WHERE bid = :bid;
        INSERT INTO pgbench_history (tid, bid, aid, delta, mtime) VALUES (:tid, :bid, :aid, :delta, CURRENT_TIMESTAMP);
        END;
        ```

4.  使用如下命令测试。

    -   只读测试：

        ``` {#codeblock_xaw_mjq_j0p}
        polar.o.x8.4xlarge，总数据量10亿，热数据1亿
        pgbench -M prepared -v -r -P 1 -f ./ro.sql -c 128 -j 128 -T 120 -D scale=10000 -D range=100000000
        polar.o.x8.4xlarge，总数据量10亿，热数据5亿
        pgbench -M prepared -n -r -P 1 -f ./ro.sql -c 128 -j 128 -T 120 -D scale=10000 -D range=500000000
        polar.o.x8.4xlarge，总数据量10亿，热数据10亿
        pgbench -M prepared -n -r -P 1 -f ./ro.sql -c 128 -j 128 -T 120 -D scale=10000 -D range=1000000000
        polar.o.x8.2xlarge，总数据量10亿，热数据1亿
        pgbench -M prepared -v -r -P 1 -f ./ro.sql -c 64 -j 64 -T 120 -D scale=10000 -D range=100000000
        polar.o.x8.2xlarge，总数据量10亿，热数据5亿
        pgbench -M prepared -n -r -P 1 -f ./ro.sql -c 64 -j 64 -T 120 -D scale=10000 -D range=500000000
        polar.o.x8.2xlarge，总数据量10亿，热数据10亿
        pgbench -M prepared -n -r -P 1 -f ./ro.sql -c 64 -j 64 -T 120 -D scale=10000 -D range=1000000000
        polar.o.x8.xlarge，总数据量10亿，热数据1亿
        pgbench -M prepared -v -r -P 1 -f ./ro.sql -c 32 -j 64 -T 120 -D scale=10000 -D range=100000000
        polar.o.x8.xlarge，总数据量10亿，热数据5亿
        pgbench -M prepared -n -r -P 1 -f ./ro.sql -c 32 -j 64 -T 120 -D scale=10000 -D range=500000000
        polar.o.x8.xlarge，总数据量10亿，热数据10亿
        pgbench -M prepared -n -r -P 1 -f ./ro.sql -c 32 -j 64 -T 120 -D scale=10000 -D range=1000000000
        polar.o.x4.xlarge，总数据量10亿，热数据1亿
        pgbench -M prepared -v -r -P 1 -f ./ro.sql -c 32 -j 32 -T 120 -D scale=10000 -D range=100000000
        polar.o.x4.xlarge，总数据量10亿，热数据5亿
        pgbench -M prepared -n -r -P 1 -f ./ro.sql -c 32 -j 32 -T 120 -D scale=10000 -D range=500000000
        polar.o.x4.xlarge，总数据量10亿，热数据10亿
        pgbench -M prepared -n -r -P 1 -f ./ro.sql -c 32 -j 32 -T 120 -D scale=10000 -D range=1000000000
        polar.o.x4.large，总数据量5亿，热数据1亿
        pgbench -M prepared -v -r -P 1 -f ./ro.sql -c 16 -j 16 -T 120 -D scale=5000 -D range=100000000
        polar.o.x4.large，总数据量5亿，热数据5亿
        pgbench -M prepared -n -r -P 1 -f ./ro.sql -c 16 -j 16 -T 120 -D scale=5000 -D range=500000000
        polar.o.x4.medium，总数据量1亿，热数据5000万
        pgbench -M prepared -v -r -P 1 -f ./ro.sql -c 8 -j 8 -T 120 -D scale=1000 -D range=50000000
        polar.o.x4.medium，总数据量1亿，热数据1亿
        pgbench -M prepared -n -r -P 1 -f ./ro.sql -c 8 -j 8 -T 120 -D scale=1000 -D range=100000000
        ```

    -   读写测试：

        ``` {#codeblock_o32_h7c_fdn}
        polar.o.x8.4xlarge，总数据量10亿，热数据1亿
        pgbench -M prepared -v -r -P 1 -f ./rw.sql -c 128 -j 128 -T 120 -D scale=10000 -D range=100000000
        polar.o.x8.4xlarge，总数据量10亿，热数据5亿
        pgbench -M prepared -n -r -P 1 -f ./rw.sql -c 128 -j 128 -T 120 -D scale=10000 -D range=500000000
        polar.o.x8.4xlarge，总数据量10亿，热数据10亿
        pgbench -M prepared -n -r -P 1 -f ./rw.sql -c 128 -j 128 -T 120 -D scale=10000 -D range=1000000000
        polar.o.x8.2xlarge，总数据量10亿，热数据1亿
        pgbench -M prepared -v -r -P 1 -f ./rw.sql -c 64 -j 64 -T 120 -D scale=10000 -D range=100000000
        polar.o.x8.2xlarge，总数据量10亿，热数据5亿
        pgbench -M prepared -n -r -P 1 -f ./rw.sql -c 64 -j 64 -T 120 -D scale=10000 -D range=500000000
        polar.o.x8.2xlarge，总数据量10亿，热数据10亿
        pgbench -M prepared -n -r -P 1 -f ./rw.sql -c 64 -j 64 -T 120 -D scale=10000 -D range=1000000000
        polar.o.x8.xlarge，总数据量10亿，热数据1亿
        pgbench -M prepared -v -r -P 1 -f ./rw.sql -c 32 -j 64 -T 120 -D scale=10000 -D range=100000000
        polar.o.x8.xlarge，总数据量10亿，热数据5亿
        pgbench -M prepared -n -r -P 1 -f ./rw.sql -c 32 -j 64 -T 120 -D scale=10000 -D range=500000000
        polar.o.x8.xlarge，总数据量10亿，热数据10亿
        pgbench -M prepared -n -r -P 1 -f ./rw.sql -c 32 -j 64 -T 120 -D scale=10000 -D range=1000000000
        polar.o.x4.xlarge，总数据量10亿，热数据1亿
        pgbench -M prepared -v -r -P 1 -f ./rw.sql -c 32 -j 32 -T 120 -D scale=10000 -D range=100000000
        polar.o.x4.xlarge，总数据量10亿，热数据5亿
        pgbench -M prepared -n -r -P 1 -f ./rw.sql -c 32 -j 32 -T 120 -D scale=10000 -D range=500000000
        polar.o.x4.xlarge，总数据量10亿，热数据10亿
        pgbench -M prepared -n -r -P 1 -f ./rw.sql -c 32 -j 32 -T 120 -D scale=10000 -D range=1000000000
        polar.o.x4.large，总数据量5亿，热数据1亿
        pgbench -M prepared -v -r -P 1 -f ./rw.sql -c 16 -j 16 -T 120 -D scale=5000 -D range=100000000
        polar.o.x4.large，总数据量5亿，热数据5亿
        pgbench -M prepared -n -r -P 1 -f ./rw.sql -c 16 -j 16 -T 120 -D scale=5000 -D range=500000000
        polar.o.x4.medium，总数据量1亿，热数据5000万
        pgbench -M prepared -v -r -P 1 -f ./rw.sql -c 8 -j 8 -T 120 -D scale=1000 -D range=50000000
        polar.o.x4.medium，总数据量1亿，热数据1亿
        pgbench -M prepared -n -r -P 1 -f ./rw.sql -c 8 -j 8 -T 120 -D scale=1000 -D range=100000000
        ```

    **说明：** 

    -   scale乘以10万：表示测试数据量。
    -   range：表示活跃数据量。
    -   -c：表示测试连接数，测试连接数不代表该规格的最大连接数，最大连接数请参考[规格与定价](../../../../cn.zh-CN/产品简介/规格与定价.md#)。

## 测试结果 {#section_lfs_dyd_l2b .section}

|规格|测试数据量|热（活跃）数据量|只读QPS|读写QPS|
|--|-----|--------|-----|-----|
| polar.o.x8.4xlarge

 32核 256G

 |10亿|1亿|522160|274270|
| polar.o.x8.4xlarge

 32核 128G

 |10亿|5亿|514143|262859|
| polar.o.x8.4xlarge

 32核 128G

 |10亿|10亿|493321|249679|
| polar.o.x8.2xlarge

 16核 128G

 |10亿|1亿|256998|145386|
| polar.o.x8.2xlarge

 16核 128G

 |10亿|5亿|253937|123806|
| polar.o.x8.2xlarge

 16核 128G

 |10亿|10亿|243326|107800|
| polar.o.x8.xlarge

 8核 64G

 |10亿|1亿|159323|66792|
| polar.o.x8.xlarge

 8核 64G

 |10亿|5亿|155498|54070|
| polar.o.x8.xlarge

 8核 64G

 |10亿|10亿|152735|54456|
| polar.o.x4.xlarge

 8核 32G

 |10亿|1亿|129323|59738|
| polar.o.x4.xlarge

 8核 32G

 |10亿|5亿|115498|49924|
| polar.o.x4.xlarge

 8核 32G

 |10亿|10亿|102735|47946|
| polar.o.x4.large

 4核 16G

 |5亿|1亿|75729|45242|
| polar.o.x4.large

 4核 16G

 |5亿|5亿|63818|40308|
| polar.o.x4.medium

 2核 8G

 |1亿|5000万|34386|19886|
| polar.o.x4.medium

 2核 8G

 |1亿|1亿|33752|18242|

**说明：** 

-   规格：POLARDB for Oracle的规格代码（提工单调整内存和RDS for PostgreSQL相同）。
-   预计默认存储空间可存储数据量：预计该规格默认存储空间可以存储的记录条数。
-   测试数据量：本轮测试数据的记录条数。
-   热（活跃）数据量：本轮测试的查询、更新SQL的记录条数。
-   只读QPS：只读测试的结果，表示每秒请求数。
-   读写QPS：读写测试的结果，表示每秒请求数。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/217766/155747911047060_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/217766/155747911047061_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/217766/155747911047062_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/217766/155747911047063_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/217766/155747911047064_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/217766/155747911047065_zh-CN.png)

