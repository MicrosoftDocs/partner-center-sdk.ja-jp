---
title: Service costs resources
description: Describes resources related to services purchased by a customer.
ms.assetid: 2916B7F3-06D5-4DC1-A137-CD8270258CDB
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: a7d08c740e0a338e1c8b09908b346257f60fe444
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488082"
---
# <a name="service-costs-resources"></a>Service costs resources

適用対象:

- パートナー センター

Describes resources related to services purchased by a customer.

## <a name="servicecostssummary"></a>ServiceCostsSummary

**ServiceCostsSummary** contains a summary that aggregates all services purchased by the specified customer during the billing period.

| プロパティ | タスクバーの検索ボックスに | 説明 |
| -------- | ---- | ----------- |
| details | array of [ServiceCostsSummaryDetail](#servicecostssummarydetail) objects | The service cost summary detail list, distinguished by invoice type.|
| links | [ResourceLinks](utility-resources.md#resourcelinks) | The resource links. |
| 属性 | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. |

> [!IMPORTANT]
> **The fields in the following table are being deprecated.** To retrieve recurring and one-time service cost summaries, use the **details** field instead. The **details** field is described in the previous table. Refer to the **details** field's corresponding data values but not the root-level fields.

| プロパティ | タスクバーの検索ボックスに | 説明 |
| -------- | ---- | ----------- |
| billingStartDate | date | The start of the billing period. |
| billingEndDate | date | The end of the billing period. |
| pretaxTotal | double | The pre-tax total of all costs for the customer. |
| 税金  | double | The total tax incurred over all items purchased by the customer. |
| afterTaxTotal | double | The net total cost for all items purchased by the customer. |
| currencyCode | string | Represents the currency used for the costs. |
| currencySymbol | string | The currency symbol used for the costs. |
| customerId | string | The ID of the customer making the purchase. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**ServiceCostsSummaryDetail** describes a service cost summary that aggregates all services purchased by the specified customer during the billing period (from either recurring or one-time invoices).

| プロパティ | タスクバーの検索ボックスに | 説明 |
| -------- | ---- | ----------- |
| invoiceType | string | The invoiceType that service cost summary has been generated. |
| summary | [ServiceCostsSummary](#servicecostssummary) | The service cost summary aggregated by a customer under one invoice type. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**ServiceCostLineItem** describes a single item purchased by the customer.

> [!IMPORTANT]
> The following properties *only apply to* service cost line items where the product is a *one-time purchase*: **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**. These properties *don't apply to* service line items where the product is a *recurring purchase*. For example, these properties *don't apply* to subscription-based Office 365 and Azure.

| プロパティ                 | タスクバーの検索ボックスに                           | 説明                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| startDate                | string in UTC date-time format | The start date for the charge.                                       |
| endDate                  | string in UTC date-time format | The end date for the charge.                                         |
| subscriptionFriendlyName | string                         | The friendly name for the subscription.                              |
| subscriptionId           | string                         | The subscription identifier.                                         |
| orderId                  | string                         | The order identifier.                                                |
| offerId                  | string                         | The offer identifier.                                                |
| offerName                | string                         | The offer name.                                                      |
| resellerMPNId            | string                         | Only used in 2-tier partner scenarios. Refers to the MPN identifier. |
| chargeType               | string                         | The associated charge type.                                          |
| quantity                 | number                         | The quantity of units used or purchased.                             |
| unitPrice                | number                         | The price per unit.                                                  |
| pretaxTotal              | number                         | The total charge for this item before taxes.                         |
| 税金                      | number                         | The total tax charge incurred for this item.                         |
| afterTaxTotal            | number                         | The net total cost for this item.                                    |
| currencyCode             | string                         | Represents the currency used for the costs.                          |
| currencySymbol           | string                         | The currency symbol used for the costs.                              |
| customerId               | string                         | The ID of the customer making the purchase.                          |
| customerName             | string                         | The name of the customer making the purchase.                        |
| invoiceNumber            | string                         | The invoice number that this line item belongs to.                   |
| productId                | string                         | The product identifier.                                              |
| skuId                    | string                         | The Sku identifier.                                                  |
| availabilityId           | string                         | The availability identifier.                                         |
| productName              | string                         | The product name.                                                    |
| skuName                  | string                         | The sku name.                                                        |
| publisherName            | string                         | The publisher name.                                                  |
| publisherId              | string                         | The publisher identifier.                                            |
| termAndBillingCycle      | string                         | The term and billing cycle.                                          |
| discountDetails          | string                         | The discount details.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| プロパティ             | タスクバーの検索ボックスに                               | 説明                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Link](utility-resources.md#link) | The URI to retrieve the line items. |
| self                 | [Link](utility-resources.md#link) | The self URI.                       |
