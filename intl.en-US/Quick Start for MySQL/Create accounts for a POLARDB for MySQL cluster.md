# Create accounts for a POLARDB for MySQL cluster {#concept_ew4_wmq_tdb .concept}

POLARDB for MySQL supports two types of accounts: privileged accounts and standard accounts. You can manage all accounts in the POLARDB console.

**Note:** For security purposes, POLARDB does not support the root accounts.

|Account type|Description|
|------------|-----------|
|**Privileged accounts**| -   You can create and manage privileged accounts only in the POLARDB console.
-   Each POLARDB cluster can have only one privileged account. This privileged account has the permissions to manage all standard accounts and databases in the cluster.
-   More permissions are granted to a privileged account to achieve finer permission management such as granting the query permissions for tables by user.
-   The privileged account of a POLARDB cluster has the permissions for all databases in the cluster.
-   The privileged account of a POLARDB cluster can disconnect any account from the cluster.

 |
|**Standard accounts**| -   You can create and manage standard accounts in the POLARDB console or by using SQL statements.
-   Each POLARDB cluster can have one or more standard accounts depending on the number of database cores.
-   You must manually grant the permissions for databases to standard accounts.
-   A standard account of a POLARDB cluster does not have the permissions to create or manage other accounts or disconnect other accounts from the cluster.

 |

## Create a privileged account {#section_ktr_gqv_tdb .section}

1.  Log on to [POLARDB console](https://polardb.console.aliyun.com).
2.  Find the target POLARDB cluster and click its ID.
3.  In the left-side navigation pane, click **Accounts**.
4.  Click **Create Account**.
5.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Account Name**| Enter the name of the privileged account. The account name:

     -   Must begin with a letter and end with a letter or digit.
    -   Can contain lowercase letters, digits, and underscores \(\_\).
    -   Must be 2 to 16 characters in length.
    -   Cannot be any reserved username, such as **root** and **admin**.
 |
    |**Account Type**|Select **Privileged Account**. **Note:** If a privileged account already exists, you cannot select **Privileged Account** because each POLARDB cluster can have only one privileged account.

 |
    |**Password**|Enter the password of the privileged account. The password:     -   Must contain at three of the following types of characters: uppercase letters, lowercase letters, digits, and special characters.
    -   Must be 8 to 32 characters in length.
    -   Must support only the following special characters:

! @ \# $ % ^ & \* \( \) \_ + - =

 |
    |**Confirm Password**|Re-enter the password.|
    |**Description**|Enter the relevant account information for easy account management. The description:     -   Cannot start with **http://** or **https://**.
    -   Must start with a letter.
    -   Can contain uppercase letters, lowercase letters, digits, underscores \(\_\), and hyphens \(-\).
    -   Must be 2 to 256 characters in length.
 |


## Create a standard account {#section_nym_xr5_q2b .section}

1.  Log on to the [POLARDB console](https://polardb.console.aliyun.com).
2.  Find the target POLARDB cluster and click its ID.
3.  In the left-side navigation pane, click **Account**s.
4.  Click **Create Account**.
5.  Set the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Account Name**|Enter the name of the standard account. The account name:     -   Must begin with a letter and end with a letter or digit.
    -   Can contain lowercase letters, digits, and underscores \(\_\).
    -   Must be 2 to 16 characters in length.
    -   Cannot be any reserved username, such as **root** and **admin**.
 |
    |**Account Type**|Select **Standard Account**.|
    |**Databases**|Grant the permissions for one or more databases to the standard account. This parameter is optional. You can grant permissions to the standard account after you create it.     1.  Select one or more databases from the left section and click the right arrow to add them to the right section.
    2.  In the right section, select **Read&Write**,**ReadOnly**, or**DMLOnly** permissions for each database.
 |
    |**Password**|Enter the password of the standard account. The password:     -   Must contain at three of the following types of characters: uppercase letters, lowercase letters, digits, and special characters.
    -   Must be 8 to 32 characters in length.
    -   Must support only the following special characters:

! @ \# $ % ^ & \* \( \) \_ + - =

 |
    |**Confirm Password**|Re-enter the password.|
    |**Description**|Enter the relevant account information for easy account management. The description:     -   Cannot start with **http://** or **https:/**/.
    -   Must start with a letter.
    -   Can contain uppercase letters, lowercase letters, digits, underscores \(\_\), and hyphens \(-\).
    -   Must be 2 to 256 characters in length.
 |

6.  Click **OK**.

## Reset the permissions of a privileged account {#section_lhq_ybt_zfb .section}

If the privileged account of a POLARDB cluster encounters a problem \(for example, the permissions are revoked by mistake\), you can enter the password of the privileged account to reset permissions.

1.  Log on to the [POLARDB console](https://polardb.console.aliyun.com).
2.  Find the target POLARDB cluster and click its ID.
3.  In the left-side navigation pane, click **Accounts**.
4.  Find the privileged account and in the **Actions** column click **Reset Permissions**.
5.  In the displayed dialog box, enter the password of the privileged account and click **OK**.

## APIs {#section_vdj_5tl_ggb .section}

|API|Description|
|:--|:----------|
|[CreateAccount](../../../../intl.en-US/API Reference/Account management/CreateAccount.md#)|Used to create an account.|
|[DescribeAccounts](../../../../intl.en-US/API Reference/Account management/DescribeAccounts.md#)|Used to list accounts.|
|[ModifyAccountDescription](../../../../intl.en-US/API Reference/Account management/ModifyAccountDescription.md#)|Used to modify the description of an account.|
|[ModifyAccountPassword](../../../../intl.en-US/API Reference/Account management/ModifyAccountPassword.md#)|Used to change the password of an account.|
|[GrantAccountPrivilege](../../../../intl.en-US/API Reference/Account management/GrantAccountPrivilege.md#)|Used to grant permissions to an account.|
|[RevokeAccountPrivilege](../../../../intl.en-US/API Reference/Account management/RevokeAccountPrivilege.md#)|Used to revoke the permissions of an account.|
|[ResetAccount](../../../../intl.en-US/API Reference/Account management/ResetAccount.md#)|Used to reset the permissions of an account.|

