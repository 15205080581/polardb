# Version of the PolarDB database kernel

This topic describes the parts of a version of the PolarDB database kernel and relationships between the parts.

A full version of the PolarDB database kernel consists of three parts: DB version, minor version, and revision version. The following figure shows the relationship among the three parts. In the following example, the DB version is 8.0.

![Version description](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5650688951/p142635.png)

The DB version is the most important identification number that is used to identify a version of the PolarDB database kernel. The DB version has one or more minor versions. For example, DB version 5.6 has only minor version 5.6, and DB version 8.0 has minor versions 8.0.1 and 8.0.2. Features vary based on minor versions. We recommend that you select a minor version based on your business requirements before you purchase a cluster. In most cases, a minor version has multiple revision versions. In the latest revision version, existing features are optimized or simple features are added. In minor versions and revision versions, security and performance are improved.

**Note:** The latest version of the PolarDB database kernel is compatible with earlier versions and includes all the features of the earlier versions. Therefore, you do not need to modify your applications after you upgrade kernel versions. For more information about how to upgrade kernel versions, see [Version upgrade](/intl.en-US/.md).

