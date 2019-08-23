# 诊断慢SQL {#concept_xc2_4qr_2gb .concept}

您可以根据日期查看集群或节点中数据库的慢SQL统计，或者根据时间段更进一步的查看节点中的慢SQL明细，并且提供SQL建议和诊断分析。

## 操作步骤 {#section_f4b_sb3_mfb .section}

1.  进入[POLARDB控制台](https://polardb.console.aliyun.com/)。
2.  选择地域。
3.  找到目标集群，单击集群名称列的**集群ID**。
4.  在左侧导航栏中选择**诊断与优化** \> **慢SQL**。
5.  您可以根据需要查看慢SQL统计或慢SQL明细。
    -   慢SQL统计：
        1.  右上角选择集群或节点，左侧选择慢SQL统计并选择日期和数据库，单击**查询**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81392/156594452334860_zh-CN.png)

        2.  单击SQL语句列的慢SQL语句，单击**SQL建议**查看索引建议，或者单击**诊断分析**跳转到[SQL调优](intl.zh-CN/POLARDB for MySQL用户指南/诊断与优化/问题分析/SQL调优.md#)进行诊断。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81392/156594452434861_zh-CN.png)

    -   慢SQL明细：
        1.  右上角选择节点，左侧选择慢SQL明细并选择时间段，单击**确定**。

            **说明：** 开始时间和结束时间间隔范围为3小时。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/81392/156594452434862_zh-CN.png)

        2.  单击SQL语句列的慢SQL语句，单击**SQL建议**查看索引建议，或者单击**诊断分析**跳转到[SQL调优](intl.zh-CN/POLARDB for MySQL用户指南/诊断与优化/问题分析/SQL调优.md#)进行诊断。

