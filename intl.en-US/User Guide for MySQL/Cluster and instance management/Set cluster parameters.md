# Set cluster parameters {#concept_isq_zgy_ydb .concept}

This topic describes how to modify parameter values of a cluster in the ApsaraDB for POLARDB console. For more information about the parameters, see [Server System Variables](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html).

## Important notes {#section_jgg_4jy_ydb .section}

-   You must modify parameter values according to the **Value Range** column on the Parameters page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/14001/156594099913713_en-US.png)

-   For some parameters, you need to restart all nodes after the parameter values are modified. We recommend that you make appropriate service arrangements before you restart the nodes. Proceed with caution. You can determine whether the modification of a parameter value requires a node restart according to the value in the **Force Restart** column on the **Parameters** page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/14001/156594099913711_en-US.png)


## Procedure {#section_osq_bhy_ydb .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Find the target cluster and click the cluster ID in the **Cluster Name** column.
4.  In the left-side navigation pane, choose **Settings and Management** \> **Parameters**.
5.  Modify the values of one or more parameters in the **Current Value** column, and click **Apply Changes**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/14001/156594100034687_en-US.png)

6.  In the Save Changes dialog box that appears, click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/14001/156594100034688_en-US.png)


## Related API operations {#section_ydc_t4h_yfb .section}

|API operation|Description|
|:------------|:----------|
|[DescribeDBClusterParameters](../../../../intl.en-US/API Reference/Cluster parameters/DescribeDBClusterParameters.md#)|Views cluster parameters.|
|[ModifyDBClusterParameters](../../../../intl.en-US/API Reference/Cluster parameters/ModifyDBClusterParameters.md#)|Modifies the values of cluster parameters.|

