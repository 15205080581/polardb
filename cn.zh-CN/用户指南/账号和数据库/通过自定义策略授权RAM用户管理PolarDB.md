# 通过自定义策略授权RAM用户管理PolarDB

如果RAM提供的系统策略无法满足您的业务需求，您可以通过创建自定义策略对云数据库PolarDB进行精细化权限管理（例如资源或操作级别的授权）。

使用RAM进行权限管理前，请确保您已完成[账号注册](https://account.aliyun.com/register/register.htm)。

-   权限策略是用语法结构描述的一组权限的集合，可以精确地描述被授权的资源集、操作集以及授权条件，详细的语言规范请参见[权限策略语法和结构](https://help.aliyun.com/document_detail/93739.html)。
-   使用自定义策略对PolarDB进行精细化权限管理前，请先了解PolarDB的权限定义，详情请参见[RAM资源授权](/cn.zh-CN/API参考/RAM资源授权.md)。

**说明：** 如果需要自定义各种权限类型组合或授予某些表级别权限等场景，您可以通过数据管理DMS推出的数据库账号权限管理功能进行灵活管控，详情请参见[MySQL数据库账号权限管理]()。

## 步骤一：创建自定义权限策略

1.  登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  在左侧导航栏，单击**权限管理** \> **权限策略管理**。

3.  单击**创建权限策略**。

4.  在**新建自定义权限策略**，配置自定义策略信息。

    ![新建自定义策略](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0830359951/p76495.png)

    |配置|说明|
    |--|--|
    |策略名称|建议填入具备业务意义的名称以便后续识别。|
    |备注（可选）|填入该策略的备注信息。|
    |配置模式|PolarDB仅支持**脚本配置**，此处选择为**脚本配置**。|
    |策略内容|下拉选择系统已有的策略，将其导入至本策略中。 **说明：** 本案例介绍自定义策略，此选项无需配置。 |
    |策略编辑框|填入具体的权限策略信息，表格下方为您列出了一些常见的自定义权限策略供您参考。 **说明：**

    -   权限策略是用语法结构描述的一组权限的集合，可以精确地描述被授权的资源集、操作集以及授权条件，详细的语言规范请参见[权限策略语法和结构](https://help.aliyun.com/document_detail/93739.html)。
    -   当前支持资源（Resource）和操作（Action）级别的授权。 |

    常见的自定义权限策略：

    -   示例1：授权目标RAM用户管理2个指定的PolarDB集群。

        假设您的账号下拥有多个PolarDB集群，但作为RAM管理员，您希望仅授权其中的2个集群（集群ID分别为i-001和i-002）给目标RAM用户，那么您可以创建如下权限策略：

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

        **说明：**

        -   被授予该权限策略的RAM用户号可以查看所有的集群及资源，但只能管理已被授权的2个集群（即集群i-001和集群i-002）。同时作为RAM管理员，您仍然可以使用API、CLI或SDK直接管理上述两个集群。
        -   `Describe*`在权限策略中是必须的，否则被授权的RAM用户无法在控制台看到任何集群。
    -   示例2：仅授权PolarDB的部分功能给目标RAM用户。

        假设您希望仅授权PolarDB的部分功能给目标RAM用户，则可以创建如下权限策略：

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

        **说明：**

        -   被授予该权限策略的目标RAM用户仅可以对账号下所有的PolarDB集群进行集群信息查询、备份查询、创建备份、删除备份、修改白名单操作，但不允许进行其他任何操作。
        -   PolarDB支持通过RAM进行API级别的访问控制，您可以通过相关API对PolarDB进行细粒度的权限访问控制，详情请参见[支持RAM的云服务](https://help.aliyun.com/document_detail/28630.html?spm=5176.11065259.1996646101.searchclickresult.587032086ReAdu)和[API概览](/cn.zh-CN/API参考/API概览.md)。
5.  单击**确定**。


## 步骤二：为RAM用户授权自定义策略

1.  登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  在左侧导航栏单击**授权管理** \> **权限策略管理**。

3.  在**权限策略管理**页，找到目标自定义权限策略，单击权限策略名称。

    ![找到名称](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0830359951/p147422.png)

4.  在目标权限策略的**基本信息**页，单击**引用记录**页签。

5.  单击**新增授权**，在弹出的对话框中，设置以下参数。

    |参数|说明|
    |--|--|
    |**授权范围**|您可以选择**授权范围**为**云账号全部资源**或**指定资源组**。|
    |**被授权主体**|您可以在搜索框内输入目标RAM用户、用户组或RAM角色名称进行模糊搜索，并在搜索结果中选择目标RAM用户。|
    |**选择权限**|目标自定义权限策略默认已加入右侧**已选择**框中，若您还需为目标RAM用户添加其他权限，可在左边待选框中选中对应的权限策略名称加入右侧**已选择**框。**说明：** 每次最多添加5条策略，如需添加更多策略，请分多次进行。 |

6.  单击**确定**。

    **说明：** 更多为RAM用户或用户组授权的方式，请参见[为RAM用户授权](/cn.zh-CN/用户管理/为RAM用户授权.md)和[为用户组授权](/cn.zh-CN/用户组管理/为用户组授权.md)。


