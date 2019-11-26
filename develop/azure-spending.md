---
title: Azure 利用状況
description: CSP partners can use Partner Center APIs to view and manage their Azure spending. They can also programmatically view their customers' Azure spending against their budget.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: d4db9a7c8c52b33618652aa5bfaf1fb00d24c49b
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489122"
---
# <a name="azure-spending"></a>Azure 利用状況

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Cloud Solution Provider (CSP) partners can view and manage their Azure spending through Partner Center APIs. They can also programmatically view their customers' spending against an Azure spending budget.

For more information, see [scenarios in which CSP partners can use the Partner Center APIs to manage customer and partner accounts and orders](scenarios.md), specifically the [background section](scenarios.md#background).

## <a name="partner-usage-management"></a>Partner usage management

- [Get a partner usage summary](get-a-partner-usage-summary.md) using the **PartnerUsageSummary** resource
- [Get usage records for all customers](get-a-customer-s-usage-records.md) using the **CustomerMonthlyUsageRecord** resource

## <a name="customer-usage-management"></a>Customer usage management

- [Get a customer's usage summary](get-a-customer-usage-summary.md) using the **CustomerUsageSummary** resource
- [Get all subscription usage records for a customer](get-a-customer-subscription-s-usage-records.md) using the **SubscriptionMonthlyUsageRecord** resource

## <a name="subscription-usage-management"></a>Subscription usage management

- [Get a subscription usage summary](get-a-customer-subscription-usage-summary.md) using the **SubscriptionUsageSummary** resource
- [Get all monthly usage records for a subscription](get-all-monthly-usage-records-for-a-subscription.md) using the **AzureResourceMonthlyUsageRecord** resource
- [Get usage data for a subscription by resource](get-a-customer-subscription-resource-usage-records.md) using the **ResourceUsageRecord** resource
- [Get usage data for a subscription by meter](get-a-customer-subscription-meter-usage-records.md) using the **MeterUsageRecord** resource

## <a name="azure-spending-budget-management"></a>Azure spending budget management

- [Get a customer's usage budget](get-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource
- [Update a customer's usage budget](update-a-customer-s-usage-spending-budget.md) using the **CustomerUsageSummary** resource
