# Use a storage package {#concept_1375373 .concept}

ApsaraDB for POLARDB provides subscription-based storage packages to help you reduce the storage cost.

You do not need to manually configure the storage of an ApsaraDB for POLARDB cluster. The storage is automatically scaled based on the data volume. You only need to pay by hour for the actual data volume. We recommend that you subscribe to POLARDB storage packages if you have a high data volume. Compared with the pay-as-you-go \(hourly rate\) billing method, the subscription-based storage package has a more favorable price. The larger storage capacity you purchase, the larger discount you enjoy.

## Price comparison between storage packages and pay-as-you-go \(hourly rate\) {#section_5jz_71v_sb2 .section}

The following table compares the prices of storage packages and pay-as-you-go \(hourly rate\).

|Capacity \(GB\)|Price of pay-as-you-go \(hourly rate\) for Mainland China \(RMB/month\)|Price of storage packages for Mainland China \(RMB/month\)|Price of pay-as-you-go \(hourly rate\) for Hong Kong and overseas regions \(RMB/month\)|Price of storage packages for Hong Kong and overseas regions \(RMB/month\)|
|---------------|-----------------------------------------------------------------------|----------------------------------------------------------|---------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
|100|350|350|390|390|
|500|1,750|1,750|1,950|1,950|
|1,000|3,500|3,150|3,900|3,510|
|3,000|10,500|9,450|11,700|10,530|
|5,000|17,500|15,750|19,500|17,550|
|10,000|35,000|31,500|39,000|35,100|
|30,000|105,000|84,000|117,000|93,600|
|50,000|175,000|140,000|195,000|156,000|
|100,000|350,000|280,000|390,000|312,000|

## Important notes {#section_di8_to8_wvs .section}

-   You can only purchase one storage package of each type. If the capacity is insufficient, you can [upgrade the storage package](#section_pfu_whq_bq0).
-   A storage package downgrade is not currently supported.
-   A storage package can be used by all the clusters in the region specified by the **storage package type**.
-   The data volume that exceeds the capacity of a storage package is charged by the pay-as-you-go billing method. For example, you have purchased a storage package of 1,000 GB, and you have three ApsaraDB for POLARDB clusters with a storage capacity of 300 GB, 400 GB, and 500 GB, respectively. After deduction, the excess data volume 200 GB \(300 GB + 400 GB + 500 GB - 1,000 GB = 200 GB\) will be charged by the pay-as-you-go billing method. You can [view storage package deduction details](#section_bn4_sg2_uyk).

## Purchase a storage package {#section_52j_k49_33o .section}

1.  Go to the page for [purchasing an ApsaraDB for POLARDB storage package](https://common-buy.aliyun.com/?commodityCode=polardb_package#/buy).
2.  Set the parameters listed in the following table.

    |Parameter|Description|
    |---------|-----------|
    |**Resource package type**|     -   **For Mainland China**: The storage package you purchase can be used for ApsaraDB for POLARDB clusters located in Mainland China.
    -   **For Hong Kong and overseas regions**: The storage package you purchase can be used for ApsaraDB for POLARDB clusters located in Hong Kong and overseas regions.
 |
    |**Storage package specification**|The capacity of the storage package.|
    |**Subscription period**|The duration of the purchased storage package.|

    ![](images/53448_en-US.png)

3.  Click **Buy Now**.
4.  Read and agree to the service agreement by selecting the check box, and click **Pay** to complete the payment.

## View storage package deduction details {#section_bn4_sg2_uyk .section}

1.  Go to the [Expenses center](https://expense.console.aliyun.com/?#/account/home) page.

    **Note:** If the page jumps to the new version, click **Return to Expense** in the left-side navigation pane.

    ![](images/53713_en-US.png)

2.  On the Expenses center page, choose **Purchases record** \> **Purchases details** in the left-side navigation pane.
3.  Set the filter conditions and click **Query** to query ApsaraDB for POLARDB bills.

    ![](images/53624_en-US.png)

4.  Click **Details** next to the target bill record.
5.  Expand **Bill Details** to view the storage package deduction details.

    ![](images/53626_en-US.png)


## Renew or upgrade a storage package {#section_pfu_whq_bq0 .section}

1.  Go to the [Expenses center](https://expense.console.aliyun.com/?#/account/home) page.

    **Note:** If the page jumps to the new version, click **Return to Expense** in the left-side navigation pane.

    ![](images/53713_en-US.png)

2.  On the Expenses center page, choose **Resource Package Management** \> **Resource Overview** in the left-side navigation pane.
3.  Select **POLARDB Storage Package** from the drop-down list of **Products**. Set the filter conditions and click **Search** to search for the specified storage package.

    ![](images/53581_en-US.png)

4.  Renew or upgrade the storage package as required.
    -   **Renewal** 
        1.  Click **Renew** in the **Actions** column.
        2.  Select the **subscription period**. Read and agree to the service agreement by selecting the check box, and click **Pay** to complete the payment.
    -   **Upgrade** 
        1.  Click **Upgrade** in the **Actions** column.
        2.  Select the **storage package specifications**. Read and agree to the service agreement by selecting the check box, and click **Pay** to complete the payment.

## FAQ {#section_r0g_pqq_x5o .section}

-   Q: Are storage packages bound to clusters for sale?

    A: No, they are not bound. You need to purchase a storage package separately. The storage occupied by clusters in the corresponding region will be automatically charged from the storage package.

-   Q: Can a storage package be shared by multiple clusters?

    A: Yes. A storage package can be used by all the clusters in the region specified by the **resource package type** \(for Mainland China or for Hong Kong and overseas regions\).

-   Q: Can a storage package be shared by clusters with different engines?

    A: Yes. A storage package can be shared by clusters of POLARDB for MySQL, PostgreSQL, and Oracle.

-   Q: What if the capacity of my storage package is insufficient? Can I buy another one?

    A: No. Only one storage package can be purchased for each type. If the capacity is insufficient, you can [upgrade the storage package](#section_pfu_whq_bq0).

-   Q: How is the data volume that exceeds the storage package capacity charged?

    A: The data volume that exceeds the capacity of a storage package is charged by the pay-as-you-go billing method.


