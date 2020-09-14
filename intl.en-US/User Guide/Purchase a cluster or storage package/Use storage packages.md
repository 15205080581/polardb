# Use storage packages

The storage capacity of PolarDB is automatically scaled up or down based on the amount of the stored data. You do not need to manually configure the storage capacity. You need only to pay for the storage space that you use. We recommend that you purchase PolarDB storage packages if you need to store large amounts of data.

## Storage space pricing

For more information about the storage space pricing, see [Storage pricing](/intl.en-US/Pricing/Specifications and pricing.md).

## Prices of storage packages and discounts

If you need to store large amounts of data, for example, 1,000 GB data or more, storage packages are more cost-effective than the pay-as-you-go billing method. Larger discounts are provided for the storage packages that contain higher storage capacities.

If you purchase yearly subscribed storage packages, you can enjoy a 15% discount: Unit price of a yearly subscribed storage package = Unit price of a monthly subscribed storage package × 12 × 85%.

|Storage capacity \(GB\)|Mainland China|Outside Mainland China|
|Pay-as-you-go \(USD/month\)|Storage package \(USD/month\)|Pay-as-you-go \(USD/month\)|Storage package \(USD/month\)|
|-----------------------|--------------|----------------------|
|---------------------------|-----------------------------|---------------------------|-----------------------------|
|100|56|55\(about 1.7% off\)

|62|61\(about 1.6% off\) |
|200|112|109\(about 2.7% off\)

|124|121\(about 2.4% off\) |
|300|168|163\(about 3.0% off\)

|186|182\(about 2.2% off\) |
|500|280|271\(about 3.2% off\)

|310|302\(about 2.6% off\) |
|1,000|560|490\(12.5% off\)

|620|550\(about 11.3% off\) |
|2,000|1,120|980\(12.5% off\)

|1,240|1,090\(about 12.1% off\) |
|3,000|1,680|1,210\(about 28.0% off\)

|1,860|1,340\(about 28.0% off\) |
|5,000|2,800|2,020\(about 28.0% off\)

|3,100|2,230\(about 28.1% off\) |
|10,000|5,600|3,260\(about 41.8% off\)

|6,200|3,630\(about 41.5% off\) |
|20,000|11,200|6,510\(about 41.9% off\)

|12,400|7,250\(about 41.5% off\) |
|30,000|16,800|9,760\(about 42.0% off\)

|18,600|10,870\(about 41.5% off\) |
|50,000|28,000|14,860\(about 47.0% off\)

|31,000|16,550\(about 46.6% off\) |
|100,000|56,000|29,720\(about 47.0% off\)

|62,000|33,110\(about 46.6% off\) |

## Considerations

-   You can purchase only one storage package of each type.
-   You are charged for the extra storage space that is not covered by the storage package on a pay-as-you-go basis. An example is used to explain the pricing details. In this example, you have three PolarDB clusters, and each of the clusters requires 400 GB of storage capacity. You purchase a storage package of 1,000 GB, and the three clusters share the storage package. In this scenario, you are charged for the extra 200 GB storage capacity on a pay-as-you-go basis. .

**Note:** For more information about storage packages, see [FAQ](#section_r0g_pqq_x5o).

## Purchase a storage package

1.  Log on to the [PolarDB console](https://polardb.console.aliyun.com/).

2.  On the top of the page, select the region where the target cluster is located.

3.  In the upper-left corner of the page, click **Create Cluster**.

4.  Click the **Storage Package** tab, and specify the following parameters.

    ![Storage package](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7310500061/p148295.png)

    |Parameter|Description|
    |---------|-----------|
    |**Package Type**|    -   **Mainland China**: The storage package can be shared by all the PolarDB clusters that reside in regions in mainland China, such as China \(Hangzhou\), China \(Shanghai\), and China \(Beijing\).
    -   **Outside Mainland China**: The storage package can be shared by all the PolarDB clusters that reside in regions outside mainland China, such as China \(Hong Kong\), UK \(London\), and Singapore \(Singapore\). |
    |**Package Specification**|The storage capacity that is provided by the storage package.|
    |**Purchase Plan**|The validity period of the storage package.**Note:** If you purchase yearly subscribed storage packages, you can enjoy a 15% discount: Unit price of a yearly subscribed storage package = Unit price of a monthly subscribed storage package × 12 × 85%. For more information, see[Prices of storage packages and discounts](#section_5jz_71v_sb2). |

5.  Click **Buy Now**.

6.  Read and agree to the service agreement. To agree to the service agreement, select the check box. Then, click **Pay** to complete the payment.


## View the database storage usage

1.  Log on to the [PolarDB console](https://polardb.console.aliyun.com/).

2.  On the top of the page, select the region where the target cluster is located.

3.  Find the target cluster and click the cluster ID to go to the Overview page.

4.  On the page, check the value of the **Database Storage Usage** field in the **Distributed Database Storage** section.

    ![Database storage usage](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7728449951/p94091.png)

    **Note:** The maximum storage capacity varies based on cluster specifications. If 90% of the maximum storage capacity is used, the system sends SMS messages and emails to you on a daily basis. If you want to increase the maximum storage capacity, scale up your cluster specifications. For more information, see [Change specifications](/intl.en-US/User Guide/Elastic upgrade and downgrade/Change specifications.md).


## FAQ

-   Are storage packages bound to clusters for sale?

    No, storage packages are not bound to clusters for sale. You must purchase storage packages separately. The storage space that is used by the clusters in the related regions is automatically deducted from the storage package.

-   Can multiple clusters share a storage package?

    Yes, multiple clusters can share a storage package. A storage package can be shared by all the clusters in the regions that are specified by the **Package Type** parameter. The value of the parameter can be Mainland China or Outside Mainland China.

-   Can clusters that use different engines share a storage package?

    Yes, clusters that use different engines can share a storage package. A storage package can be shared by PolarDB for MySQL, PolarDB for PostgreSQL, and PolarDB-O clusters.

-   How does the storage capacity that exceeds the storage capacity of my storage package incur fees?

    The storage capacity that exceeds the storage capacity of your storage package incurs fees based on the pay-as-you-go billing method. For more information, see [Storage pricing](/intl.en-US/Pricing/Specifications and pricing.md).


