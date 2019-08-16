# Change specifications {#concept_fzq_svf_xdb .concept}

You can change the specifications of your cluster to meet business requirements. POLARDB supports capacity scaling in three dimensions:

-   **Scale up or down the computing capacity**: Upgrade or downgrade the specifications of a cluster. \[DO NOT TRANSLATE\]

-   **Scale in or out the computing capacity**: Add or delete read-only instances. For more information about the detailed procedures, see [Add or delete read-only instances](intl.en-US/User Guide for MySQL/Cluster and instance management/Add or remove a node.md).

-   **Scale in or out the storage capacity**: The storage capacity is provisioned in a serverless model. As your data increases in size, the storage is automatically expanded.


This topic describes how to upgrade or downgrade the specifications of a POLARDB cluster. It will take only 5-10 minutes for the new specification of each instance to take effect.

**Note**

-   Specification upgrades or downgrades only apply to clusters. You cannot change the specifications of an instance.

-   The specification upgrades or downgrades will not affect the existing data in the cluster.

-   We recommend that you modify cluster specifications during your service off-peak periods. During a specification upgrade or downgrade, the POLARDB service will be disconnected for a few seconds and some of the functions will be disabled. You will need to reconnect from your applications once POLARDB is disconnected.

-   You can only change cluster specifications when the cluster does not have pending specification changes..


**Procedure**

1.  Log on to the [POLARDB console](https://polardb.console.aliyun.com/).
2.  Select a region.
3.  Select **Clusters**, and find your targeted cluster. Click **More**in the **Actions** column of the specific cluster, and then select **Upgrade Cluster** or **Downgrade Cluster**.
4.  Select a specification.

    **Note:** All instances in a cluster have the same specifications.

5.  Read and accept the **Terms of Service**, and click **Pay Now**.

    **Note:** It will take only 5-10 minutes for the new specification of each instance to take effect.


