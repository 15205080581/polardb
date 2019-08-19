# Configuration change fees {#concept_269560 .concept}

This topic describes the fees for changing the configuration of pay-as-you-go and subscription clusters.

## Pay-as-you-go {#section_e1p_s4y_uqb .section}

Pay-as-you-go clusters are billed by hour. After the configuration of a pay-as-you-go cluster changes, the cluster is billed at the new price by hour.

## Subscription {#section_x16_us8_z4d .section}

|Configuration change|Billing description|
|--------------------|-------------------|
|Upgrade configuration or add nodes|Payment = Total fees of the new configuration for the remaining subscription period \(The monthly price of the new configuration/30/24 × The remaining hours\) - Total fees of the original configuration for the remaining subscription period \(The monthly price of the original configuration/30/24 × The remaining hours\). Example: The monthly price of the new configuration is RMB 14,400. The monthly price of the original configuration is RMB 7,200. The remaining subscription period is 50 days. The payment is calculated as follows: \(14,400/30/24 × 50 × 24\) - \(7,200/30/24 × 50 × 24\) = RMB 12,000.

 |
|Downgrade configuration or delete nodes|Refund = Total fees of the original configuration for the remaining subscription period \(The monthly price of the original configuration/30/24 × The remaining hours\) - Total fees of the new configuration for the remaining subscription period \(The monthly price of the new configuration/30/24 × The remaining hours\). Example: You subscribed to a cluster for three months, during which the original configuration charged RMB 3,500. You paid RMB 3,000 after using coupons. After two months, the total fees of the original configuration for the remaining month are RMB 1,000. The total fees of the new configuration for a month are RMB 800. The refund is calculated as follows: 1000 - 800 = RMB 200.

 **Note:** You can be refunded for downgrading the configuration of a subscription cluster, but cannot be refunded for the whole cluster. If you need to be refunded for the whole cluster, open a ticket to submit an application. If your application is approved, your subscription cluster is frozen and will be deleted in 14 days.

 |

**Note:** If you upgrade the configuration of a cluster and then downgrade the configuration, you may get fewer refunds in the following two scenarios:

-   You used discounts in the upgrade order: For example, you subscribed to the cluster for a year at a 15% discount, which means you only need to pay RMB 850 to enjoy RMB 1,000 worth of service. Then, a refund for downgrading the configuration is calculated based on RMB 850.
-   You used coupons in the upgrade order: When you downgrade the configuration of the cluster, the refund of the original configuration is calculated based on the cash you paid, excluding the amount deducted by coupons. However, when you upgrade the configuration of the cluster, the fees of the original configuration are calculated based on the unit price of the original configuration, including the amount deducted by coupons.

## Related documents {#section_pda_8zp_zmp .section}

[Change specifications](../../../../intl.en-US/User Guide for MySQL/Cluster and instance management/Change specifications.md#)

