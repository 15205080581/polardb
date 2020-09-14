# Authorize RAM users to manage PolarDB by using custom policies

This topic describes how to authorize RAM users to manage PolarDB by using custom policies. If the system policies that are provided by Resource Access Management \(RAM\) cannot meet your business requirements, you can create custom policies for fine-grained PolarDB permission management. For example, you can create custom policies to grant permissions on specific resources and operations.

Before you use RAM to manage permissions, your Alibaba Cloud account is registered. If you have no Alibaba Cloud account, [register an Alibaba Cloud account](https://account.alibabacloud.com/register/intl_register.htm).

-   A policy defines a set of permissions that are described based on the policy structure and syntax. A policy describes the authorized resource sets, the authorized operation sets, and the authorization conditions. For more information, see [Policy structure and syntax](https://www.alibabacloud.com/help/zh/doc-detail/93739.htm).
-   Before you use custom policies for fine-grained PolarDB permission management, familiarize yourself with how to specify PolarDB resources for RAM users in policies. For more information, see [RAM resource authorization](/intl.en-US/API Reference/RAM resource authorization.md).

## Step 1: Create a custom policy

1.  Log on to the [RAM console](https://ram.console.aliyun.com/) by using an Alibaba Cloud account.

2.  In the left-side navigation pane, choose **Permissions** \> **Policies**.

3.  On the Policies page, click **Create Policy**.

4.  On the Create Custom Policy page, specify the parameters.

    ![Create a custom policy](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2083097951/p76495.png)

    |Parameter|Description|
    |---------|-----------|
    |Policy Name|Enter an informative name for easy identification.|
    |Note|Optional. Enter the description of the policy.|
    |Configuration Mode|Select **Script**. PolarDB supports only the **Script** configuration mode.|
    |Policy Document|Select an existing system policy from the drop-down list. **Note:** This topic describes how to create a custom policy. You do not need to specify this parameter. |
    |Code Editor|Enter the content of the policy in the code editor. Sample custom policies are provided for your reference below this table. **Note:**

    -   A policy defines a set of permissions that are described based on the policy structure and syntax. A policy describes the authorized resource sets, the authorized operation sets, and the authorization conditions. For more information, see [Policy structure and syntax](https://www.alibabacloud.com/help/zh/doc-detail/93739.htm).
    -   You can grant permissions on specific resources and actions. |

    Sample custom policies:

    -   Example 1: Authorize a RAM user to manage the two specified PolarDB clusters.

        Assume that you have multiple PolarDB clusters under your Alibaba Cloud account. You want to authorize a RAM user to use only two clusters whose IDs are i-001 and i-002. In this case, you can create the following policy:

        ```
        {
          "Statement": [
            {
              "Action": "polardb:*",
              "Effect": "Allow",
              "Resource": [
                          "acs:polardb:*:*:dbinstance/i-001",
                          "acs:polardb:*:*:dbinstance/i-002"
                          ]
            },
            {
              "Action": "polardb:Describe*",
              "Effect": "Allow",
              "Resource": "*"
            }
          ],
          "Version": "1"
        }
        ```

        **Note:**

        -   The authorized RAM user can view all the clusters and resources, but can manage only the two clusters whose IDs are i-001 and i-002. You can still manage the two clusters by using API operations, command-line interfaces \(CLIs\), or software development kits \(SDKs\).
        -   The policy must include `Describe*`. Otherwise, the authorized RAM user cannot view clusters in the PolarDB console.
    -   Example 2: Authorize a RAM user to use only partial features of PolarDB.

        If you want to authorize a RAM user to use only partial features of PolarDB, you can create the following policy:

        ```
        {
            "Statement": [
                {
                    "Action": [
                      "polardb:Describe*",
                      "polardb:CreateBackup",
                      "polardb:DeleteBackup",
                      "polardb:ModifyDBClusterAccessWhitelist"
                    ],
                    "Resource": "*",
                    "Effect": "Allow"
                }
            ],
            "Version": "1"
        }
        ```

        **Note:**

        -   The authorized RAM user can only query cluster information and backups, create and delete backups, and modify whitelists for all the PolarDB clusters under your account.
        -   PolarDB allows you to specify whether RAM users can perform specific operations on PolarDB resources. You can specify API operations in policies for fine-grained PolarDB permission management. For more information, see [Alibaba Cloud services that support RAM](https://help.aliyun.com/document_detail/28630.html?spm=5176.11065259.1996646101.searchclickresult.587032086ReAdu) and [List of API operations by function](/intl.en-US/API Reference/List of API operations by function.md).
5.  Click **OK**.


## Step 2: Attach the custom policy to a RAM user

1.  Log on to the [RAM console](https://ram.console.aliyun.com/).

2.  In the left-side navigation pane, choose **Permissions** \> **Policies**.

3.  On the **Policies** page, find the custom policy that you want to attach to the RAM user, and click the name of the custom policy.

    ![Find the name of the custom policy](../images/p147422.png)

4.  On the **Basic Information** page of the custom policy, click the **References** tab.

5.  Click **Grant Permission**. In the Add Permissions pane, specify the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Authorization**|Specify **Authorization** as **Alibaba Cloud account all resources** or **Specified Resource Group**.|
    |**Principal**|Enter the name of the RAM user, the user group, or the RAM role to perform a fuzzy search. Then, select the RAM user to whom you want to attach the custom policy.|
    |**Select Policy**|By default, the current custom policy appears in the **Selected** section on the right side of the pane. If you want to grant other permissions to the RAM user, select the policies in the Authorization Policy Name column on the left side of the pane. Then, the selected policies appear in the **Selected** section on the right side of the pane.**Note:** You can attach a maximum of five policies at a time. To attach more policies to the RAM user, repeat the preceding operations. |

6.  Click **OK**.

    **Note:** For more information about how to grant permissions to RAM users and RAM user groups, see [Grant permissions to a RAM user](/intl.en-US/RAM User Management/Grant permissions to a RAM user.md) and [Grant permissions to a RAM user group](/intl.en-US/RAM User Group Management/Grant permissions to a RAM user group.md).


