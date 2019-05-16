# POLARDB for MySQL常见问题 {#concept_266228 .concept}

-   删除数据库后为什么还是占用很多空间？

    答：这是由于redolog日志文件占用了空间。因为对数据的修改都会记录redolog，目前所有规格的redolog大小都为1G，待redolog上传到OSS后就会等待删除，但是等待删除的redolog会放入一个缓冲池（重命名成一个临时文件），当需要新的redolog时候，先看看缓冲池里面还有没有可用的文件，如果有直接重命名成目标文件，如果没有才会创建，这个优化主要是为了减少创建新文件时的io对系统的抖动。

    缓冲池内的redolog日志文件数量由参数**loose\_innodb\_polar\_log\_file\_max\_reuse**控制，默认是8，您可以修改这个参数从而减少日志空间占用量，但是在压力大的情况下，性能可能会出现周期性的小幅波动。

    ![loose_innodb_polar_log_file_max_reuse](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/220154/155799939647439_zh-CN.png)

    当写入大量数据后，即使redolog都被上传，默认也有8G的空间用作缓存。

    **说明：** 调整参数**loose\_innodb\_polar\_log\_file\_max\_reuse**后，缓冲池不会立刻被清空，随着DML被执行，才会慢慢减少。如果需要立即清空，请联系售后服务。

    另外，POLARDB除了当前正在写的redolog日志，还会提前创建好下一个需要写的redolog日志，而且删除redolog日志时不会清理最后一个日志，主要用来做按时间点还原任务。

    所以删除数据库后还是会占用11G空间：8G（缓冲池中的8个redolog日志）+1G（正在写的redolog日志）+1G（提前创建的redolog日志）+1G（最后一个redolog日志）。

-   磁盘空间无法选择怎么办？

    答：存储空间无需手动选择，系统根据数据量自动伸缩。

    POLARDB底层使用存储集群的方式，可以做到磁盘动态扩容，且磁盘扩容过程对用户无感知，当磁盘空间使用了70%，系统就会自动扩容一部分空间，而且扩容不需要停止实例。通过这种机制，POLARDB的存储可以做到按照使用量来收费。

-   读写分离怎么保证读一致性？

    答：读写分离链路会记录日志序号（Log sequence number，LSN），读请求会发往LSN符合要求的只读节点，详情请参见[读写分离](cn.zh-CN/POLARDB for MySQL用户指南/读写分离.md#section_rfw_ys5_j2b)。


