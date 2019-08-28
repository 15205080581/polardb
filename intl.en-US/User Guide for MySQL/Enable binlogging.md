# Enable binlogging {#concept_ekv_brx_3hb .concept}

ApsaraDB for POLARDB is a cloud native database fully compatible with MySQL. By default, it uses more advanced physical logs instead of binlogs. However, to better integrate with the MySQL ecosystem, ApsaraDB for POLARDB allows you to enable binlogging. When binlogging is enabled, you can connect to the data products such as [ElasticSearch](https://www.alibabacloud.com/help/doc-detail/90777.htm) and AnalyticDB. You can also synchronize data from POLARDB to RDS, from RDS to POLARDB, or between POLARDB clusters in a real time manner.

## Prerequisites {#section_x2h_nty_3hb .section}

The cluster was created after April 5, 2019. If the cluster was created on April 5, 2019 or earlier, you need to [open a ticket](https://selfservice.console.aliyun.com/ticket/createIndex) to perform minor version upgrade. After that, you can enable binlogging in the console.

## Pricing {#section_v2y_2ty_3hb .section}

The space used to store binlogs is a part of the cluster storage space. It is charged based on the [pricing policies](../intl.en-US/Pricing/Specifications and pricing.md#).

## Precautions {#section_ggz_dk4_kgb .section}

-   By default, the binlog files are saved for two weeks after binlogging is enabled. The binlog files that are generated more than two weeks ago are automatically deleted. You can modify the **loose\_expire\_logs\_hours** parameter to set the duration for storing binlog files. The value ranges from 0 to 2376, in hours. The value 0 indicates that the binlog files are not automatically deleted.
-   By default, the binlogging feature is disabled. To enable this feature, you need to restart the instance, which will cause service interruptions. We recommend that you arrange services appropriately before you restart an instance.
-   After binlogging is enabled, the write performance is deteriorated, while the read performance is not affected.
-   The primary endpoint directly points to the primary node that generates binlog files, ensuring higher compatibility and stability. We recommend that you use the **primary endpoint** of ApsaraDB for POLARDB when you pull, subscribe to, or synchronize binlog files by using a tool such as DTS. You can view the primary endpoint on the Basic Information page, as shown in the following figure.

    ![Primary endpoint](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/155021/156695575843468_en-US.png)


## Enable binlogging {#section_ebg_frx_3hb .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com).
2.  Select the region where the target cluster is located.
3.  Find the target cluster, and then click the cluster ID in the **Cluster Name** column.
4.  In the left-side navigation pane, choose **Settings and Management** \> **Parameters**.
5.  Search for the **loose\_polar\_log\_bin** parameter, change the value of the parameter to ON\_WITH\_GTID, and then click **Apply Changes**.

    ![Enable binlogging](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/155030/156695575843470_en-US.png)

6.  In the dialog box that appears, click **OK**.

    **Note:** If the error message **Custins minor version does not support current action** is displayed, [open a ticket](https://selfservice.console.aliyun.com/ticket/createIndex) to enable binlogging.


## FAQs {#section_k2h_cly_3hb .section}

-   Q: How long can binlog files be stored?

    A: By default, the binlog files are saved for two weeks after binlogging is enabled. The binlog files that are generated more than two weeks ago are automatically deleted. You can modify the **loose\_expire\_logs\_hours** parameter to set the duration for storing binlog files. The value ranges from 0 to 2376, in hours. The value 0 indicates that the binlog files are not automatically deleted.

-   Q: How do I disable binlogging after it is enabled?

    A: Set the **loose\_polar\_log\_bin** parameter to OFF, and then submit the changes. The existing binlog files will not be deleted after binlogging is disabled.

-   Q: What is the impact of enabling binlogging on performance?

    A: According to the test data, with 64 concurrent calls, there will be a write performance deterioration of 30% to 40% after binlogging is enabled. The write performance is optimized with the increase of concurrent calls, and will be continuously optimized in the future. The read performance will not be affected. For business scenarios with more read operations than write operations, the impact on the overall database performance is slight. For example, if the read-write ratio is 4:1, the overall performance is deteriorated by about 10%.


