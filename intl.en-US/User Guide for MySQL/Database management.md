# Database management {#concept_pqf_fy5_mfb .concept}

You can create and manage all databases in the ApsaraDB for POLARDB console.

## Create a database {#section_efz_yt5_q2b .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com).
2.  Select a region.
3.  Find the target cluster and click the cluster ID in the Cluster Name column.
4.  In the left-side navigation pane, choose **Settings and Management** \> **Databases**.
5.  Click **Create Database**.
6.  In the dialog box that appears, set parameters for creating a database. The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Database Name**|     -   It must start with a letter and end with a letter or digit.
    -   It can contain lowercase letters, digits, underscores \(\_\), and hyphens \(-\).
    -   It must be 2 to 64 characters in length.
    -   Each database name in an instance must be unique.
 |
    |**Supported Character Set**|Select utf8mb4, utf8, gbk, or latin1. You can also select other required character sets from the drop-down list on the right.

 |
    |**Authorized Account**|Select the account that you want to authorize for accessing this database. You can leave this parameter blank, and bind an account after the database is created. **Note:** Only **standard accounts** are available in the drop-down list. The privileged account has all the permissions on all databases. You do not need to authorize the privileged account to access the database that you create.

 |
    |**Account Permission**|Select the permission that you want to grant to your account. Valid values: **Read and Write**, **Read Only**, and **DML Only**.|
    |**Description**|Enter the remarks of the database to facilitate subsequent database management. The requirements are as follows:     -   The description cannot start with http:// or https://.
    -   The description must start with an uppercase or lowercase letter or a Chinese character.
    -   The description can contain uppercase or lowercase letters, Chinese characters, digits, underscores \(\_\), and hyphens \(-\).
    -   The description must be 2 to 256 characters in length.
 |

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23963/156593887634698_en-US.png)

7.  Click **OK**.

## Delete a database {#section_gwc_4tv_mfb .section}

1.  Log on to the [ApsaraDB for POLARDB console](https://polardb.console.aliyun.com).
2.  Select a region.
3.  Find the target cluster and click the cluster ID in the Cluster Name column.
4.  In the left-side navigation pane, choose **Settings and Management** \> **Databases**.
5.  Find the target database and click **Delete** in the Actions column.
6.  In the dialog box that appears, click **OK**.

## Related API operations {#section_tdx_q4h_yfb .section}

|API operation|Description|
|:------------|:----------|
|[CreateDatabase](../../../../intl.en-US/API Reference/Database management/CreateDatabase.md#)|Creates a database.|
|[DescribeDatabases](../../../../intl.en-US/API Reference/Database management/DescribeDatabases.md#)|Views the database list.|
|[ModifyDBDescription](../../../../intl.en-US/API Reference/Database management/ModifyDBDescription.md#)|Modifies the description of a database.|
|[DeleteDatabase](../../../../intl.en-US/API Reference/Database management/DeleteDatabase.md#)|Deletes a database.|

