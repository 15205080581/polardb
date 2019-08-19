# Create and authorize a RAM user {#concept_y33_t4q_tdb .concept}

You can use your Alibaba Cloud account to access your ApsaraDB for POLARDB resources.

If you want to share the resources under your Alibaba Cloud account with other users, create and authorize a Resource Access Management \(RAM\) user. The RAM user can then be used to access specified resources.

## Create a RAM user {#section_m66_z7t_pfi .section}

1.  You can use an Alibaba Cloud account or a RAM user to create one or more RAM users. First, log on to the RAM console.
    -   Click [here](https://account.alibabacloud.com/login/login.htm) to log on with your Alibaba Cloud account.

    -   Click [here](https://signin-intl.aliyun.com/login.htm) to log on with your RAM user.

**Note:** Enter the RAM username in the format of `RAM username@enterprise alias` on the logon page.

2.  In the left-side navigation pane, choose **Identities** \> **Users**.
3.  Click **Create User**.

    **Note:** You can click **Add User** to create multiple RAM users at a time.

4.  Enter the logon name and display name.
5.  In the **Access Mode** section, select **Console Password Logon**.
6.  In the **Console Password** section, select **Automatically Generate Default Password** or **Custom Logon Password**.
7.  In the **Password Reset** section, select **Required at Next Logon** or **Not Required**.
8.  In the **Multi-factor Authentication** section, select **Not Required**.
9.  Click **OK**.

## Grant permission on the Grants page {#section_gwi_ld8_aqh .section}

1.  In the left-side navigation pane, choose **Permissions** \> **Grants**.
2.  Click **Grant Permission**.
3.  In the **Principal** field, enter the username of the target RAM user, and click the RAM user.
4.  In the **Policy Name** column, select the target policy.

    **Note:** You can click **X** to revoke your selection.

5.  Click **OK**.
6.  Click **Finished**.

## Grant permission on the Users page {#section_23r_hc3_d8r .section}

1.  In the left-side navigation pane, choose **Identities** \> **Users**.
2.  In the **User Logon Name/Display Name** column, find the target RAM user.
3.  Click **Add Permissions**. Then, the username of the RAM user is automatically entered in the **Principal** field.
4.  In the **Policy Name** column, select the target policy.

    **Note:** You can click **X** to revoke your selection.

5.  Click **OK**.
6.  Click **Finished**.

## Log on as a RAM user {#section_zb2_54q_tdb .section}

**Prerequisites**: You must complete the preceding authorization procedures.

You can log on as a RAM user at the following addresses:

-   Universal logon address: [https://signin-intl.aliyun.com/login.htm](https://signin-intl.aliyun.com/login.htm).

    If you log on at the universal logon address, you must enter the RAM username and company alias manually. The address format is `RAM username@company alias`.

-   Dedicated logon address: You can view the logon address dedicated to your RAM users in the [RAM console](https://ram.console.aliyun.com).

     ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/3025/15662047006630_en-US.png) 

    The system will enter your company alias automatically if you log on using this dedicated address. You only need to enter the RAM username.


## More actions {#section_bc2_54q_tdb .section}

You can also add a RAM user to a group, assign roles to a RAM user, and authorize a user group or roles. For more information, see [RAM User Guide](https://www.alibabacloud.com/help/product/28625.htm).

