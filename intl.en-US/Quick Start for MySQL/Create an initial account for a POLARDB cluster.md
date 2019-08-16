# Create an initial account for a POLARDB cluster {#concept_ew4_wmq_tdb .concept}

An initial account can only be created on the cluster details page. The account can be used to log on to any instances of the cluster.

The initial account is an advanced user that can meet customization and sophisticated permission management requirements. An advanced user can manage databases and classic users by using[Data Management Service \(DMS\)](https://help.aliyun.com/knowledge_detail/52065.html) or SQL commands.

**Note:** The initial account cannot be deleted once created. You cannot change the account username, but can change the password.

## Procedure {#section_ktr_gqv_tdb .section}

1.  Log on to the [POLARDB console](https://polardb.console.aliyun.com).

2.  In the left-side navigation pane, click **Clusters**, and find your target cluster.

3.  Click the cluster ID, or click **Manage** in the **Actions** column.

4.  In the **Access Information** section, click **Apply for an Account**.

5.  In the dialog box that appears, enter usernames and passwords, and click **OK**.

    The username cannot exceed 16 characters in length, and cannot be system reserved usernames, such as root and admin.


**Note:** 

-   In POLARDB, you cannot create a root account because of security reasons.

-   You cannot create classic users in the POLARDB console. A classic user can be created and managed using SQL commands or DMS.

-   You cannot use the initial account to change classic user passwords. To change passwords, you must delete the classic user and recreate one.


