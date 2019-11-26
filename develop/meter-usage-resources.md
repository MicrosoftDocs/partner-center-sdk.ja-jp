---
title: Meter usage record resource
description: You can use the MeterUsageRecord resource to describe the estimated monetary cost of a subscription's meter level usage in the current billing cycle.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 003db39c92e96b12863edebb46b3e3341ffae10e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488312"
---
# <a name="meter-usage-record-resource"></a>Meter usage record resource

適用対象:

- パートナー センター

You can use the **MeterUsageRecord** resource to describe the estimated monetary cost of a subscription's meter level usage in the current billing cycle.

## <a name="meterusagerecord"></a>MeterUsageRecord

| プロパティ         | タスクバーの検索ボックスに               | 説明                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan. For Microsoft Azure (MS-AZR-0145P) subscriptions,, this value is the commerce subscription identifier. For Azure plan subscription resources, this value is the Azure plan identifier.                  |
| MeterId  | string             | Gets or sets the meter identifier.                                                        |
| MeterName          | string             | Gets or sets the meter name.                                       |
| カテゴリ               | string             | Gets or sets the Azure resource category.                                                 |
| サブカテゴリ             | string             |  Gets or sets the Azure resource sub-category.                                                     |
| QuantityUsed        | 10 進数             | Gets or sets the quantity of the Azure resource used.   |
| Unit   | string             | Gets or sets the unit of measure for the Azure resource. |
| TotalCost   | 10 進数             | Gets or sets the estimated total cost of usage. |
| CurrencyLocale   | string             | The locale in which the subscription was used. This property determines the currency that is used on the invoice. This property is available for Microsoft Azure (MS-AZR-0145P) subscriptions. |
| CurrencyCode   | string             | Gets or sets the currency code. This property is available for Azure plans.                                         |
| USDTotalCost   | 10 進数             | Gets or sets the estimated total cost in USD. This property is available for Azure plans.                                         |
| LastModifiedDate | string             | The day (in date-time format) that this record was last modified.                             |
| 属性       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |                                           |
