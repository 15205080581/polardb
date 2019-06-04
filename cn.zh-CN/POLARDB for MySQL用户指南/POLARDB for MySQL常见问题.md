# POLARDB for MySQL常见问题 {#concept_266228 .concept}

## 删除数据库后为什么还是占用很多空间？ {#section_2ui_tcb_ywu .section}

答：这是由于redolog日志文件占用了空间，通常在2G~11G左右，最多时会占用11G：8G（缓冲池中的8个redolog日志）+1G（正在写的redolog日志）+1G（提前创建的redolog日志）+1G（最后一个redolog日志）。

缓冲池内的redolog日志文件数量由参数**loose\_innodb\_polar\_log\_file\_max\_reuse**控制，默认是8，您可以修改这个参数从而减少日志空间占用量，但是在压力大的情况下，性能可能会出现周期性的小幅波动。

**说明：** 调整参数**loose\_innodb\_polar\_log\_file\_max\_reuse**后，缓冲池不会立刻被清空，随着DML被执行，才会慢慢减少。如果需要立即清空，请联系售后服务。

![loose_innodb_polar_log_file_max_reuse](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/220154/155963238347439_zh-CN.png)

## 磁盘空间无法选择怎么办？ {#section_4e1_mks_c2d .section}

答：存储空间无需手动选择，系统根据数据量自动伸缩。

POLARDB底层使用存储集群的方式，可以做到磁盘动态扩容，且磁盘扩容过程对用户无感知，当磁盘空间使用了70%，系统就会自动扩容一部分空间，而且扩容不需要停止实例。通过这种机制，POLARDB的存储可以做到按照使用量来收费。

## 读写分离怎么保证读一致性？ {#section_kkf_1k8_xff .section}

答：读写分离链路会记录日志序号（Log sequence number，LSN），读请求会发往LSN符合要求的只读节点，详情请参见[读写分离](cn.zh-CN/POLARDB for MySQL用户指南/读写分离.md#section_rfw_ys5_j2b)。

## 如何实现POLARDB的读写分离？ {#section_w36_hnf_ypf .section}

答：只需在应用程序中使用集群地址，即可根据配置的读负载节点实现读写分离。您也可以[自定义集群地址](cn.zh-CN/POLARDB for MySQL用户指南/集群管理/设置__释放自定义集群地址.md#)。

![集群地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/220154/155963238348356_zh-CN.png)

## 如果有多个只读节点，如何设置指定的ECS访问指定的只读节点? {#section_592_d3f_cah .section}

答：您可以设置[自定义集群地址](cn.zh-CN/POLARDB for MySQL用户指南/集群管理/设置__释放自定义集群地址.md#)，自行选择需要接入的只读节点，然后在ECS上使用该自定义集群地址。

## 只用了主地址，但是发现只读节点也有负载，是否主地址也支持读写分离？ {#section_23w_u0b_wvh .section}

答：主地址不支持读写分离，始终只连接到主节点。只读节点有少量QPS是正常现象，与主地址无关。

