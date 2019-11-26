---
title: Customer usage resources
description: Resources for customers with usage-based subscriptions and monthly use budgets (including CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary, and SpendingBudget).
ms.assetid: 268C7AF5-3A95-451F-8092-033A3E8126F2
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: f94168e7f56e3e6c769c5a563e516046d7cc3509
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489822"
---
# <a name="customer-usage-resources"></a>Customer usage resources

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Customers with usage-based subscriptions may have a monthly use budget. This budget sets a limit on the customer's maximum usage and allows the partner to track their usage over time.

> [!NOTE]
> Customer usage numbers are estimates (not final values), which should not be used for billing purposes.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord** represents the estimated monetary cost of a customer's usage in the current month.

| プロパティ         | タスクバーの検索ボックスに               | 説明                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Budget           | SpendingBudget     | The spending budget allocated for the customer.                          |
| PercentUsed      | 10 進数             | The percentage used out of the allocated budget.                        |
| ResourceId       | string             | The unique identifier of the resource.                                   |
| ResourceName     | string             | The name of the resource.                                                |
| TotalCost        | 10 進数             | The estimated total cost of usage for the resources in the subscription.|
| CurrencyLocale   | string             | The customer's currency locale. Available for Microsoft Azure (MS-AZR-0145P) subscriptions.            |
| CurrencyCode     | string             | Gets or sets the currency code. Available for Azure plans.           |
| USDTotalCost     | 10 進数             | Gets or sets the estimated total cost in USD. Available for Azure plans.                                         |
| IsUpgraded       | bool             | Gets or sets a value indicating whether the customer's Azure subscription is upgraded. The value **true** represents customers who have an Azure plan.                         |
| LastModifiedDate | date               | The date the usage data was last modified.                               |
| 属性       | ResourceAttributes | The metadata attributes corresponding to the usage record.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary** represents a summary of the customer's usage for an entire billing period.

| プロパティ         | タスクバーの検索ボックスに               | 説明                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Budget           | SpendingBudget     | The spending budget allocated for the customer.                                                                  |
| ResourceId       | string             | The unique identifier of the resource. In the context of CustomerMonthlyUsageRecord, this id is the customer id. |
| ResourceName     | string             | The name of the resource. In the context of CustomerMonthlyUsageRecord, this is the customer name.               |
| BillingStartDate | date               | The start date of the current billing period.                                                                    |
| BillingEndDate   | date               | The end date of the current billing period.                                                                      |
| TotalCost        | 10 進数             | The estimated total cost of usage for the resources in the subscription.                                         |
| CurrencyLocale   | string             | The customer's currency locale. Available for Microsoft Azure (MS-AZR-0145P) subscriptions.                                         |
| CurrencyCode     | string             | Gets or sets the currency code. Available for Azure plans.                                         |
| USDTotalCost     | 10 進数             | Gets or sets the estimated total cost in USD. Available for Azure plan subscription resources.                                         |
| LastModifiedDate | date               | The date the usage data was last modified.                                                                       |
| Links            | ResourceLinks      | The resource links corresponding to the usage summary.                                                           |
| 属性       | ResourceAttributes | The metadata attributes corresponding to the usage summary.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary** represents a partner-level summary of usage budgeting for all customers.

| プロパティ         | タスクバーの検索ボックスに               | 説明                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | 文字列の配列   | The list of email addresses for notifications.                                                                   |
| CustomerOverBudget | 整数          | The number of customers that are over budget.                                                                    |
| CustomersTrendingOver | 整数       | The number of customers that are close to going over budget.                                                     |
| CustomersWithUsageBasedSubscriptions  | 整数 | The number of customers with a usage-based subscription.                                               |
| ResourceId       | string             | The unique identifier of the resource. In the context of CustomerMonthlyUsageRecord, this id is the customer id. |
| ResourceName     | string             | The name of the resource. In the context of CustomerMonthlyUsageRecord, this is the customer name.               |
| BillingStartDate | date               | The start date of the current billing period.                                                                    |
| BillingEndDate   | date               | The end date of the current billing period.                                                                      |
| TotalCost        | 10 進数             | The estimated total cost of all customer usage based on current usage from the start of the billing period.      |
| CurrencyLocale   | string             | The currency locale.                                                                                             |
| LastModifiedDate | date               | The date the usage data was last modified.                                                                       |
| Links            | ResourceLinks      | The resource links corresponding to the usage summary.                                                           |
| 属性       | ResourceAttributes | The metadata attributes corresponding to the usage summary.                                                      |

## <a name="spendingbudget"></a>SpendingBudget

**SpendingBudget** represents the budget allocated to this customer for usage-based subscriptions.

| プロパティ   | タスクバーの検索ボックスに               | 説明                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Amount     | 10 進数             | The allocated budget. If the value is null, there is no spending budget allocated to this customer. |
| 属性 | ResourceAttributes | The metadata attributes corresponding to the budget.                                                |
