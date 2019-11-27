---
title: Azure 利用状況
description: CSP パートナーは、パートナーセンター Api を使用して、Azure の支出を表示および管理できます。 また、顧客の Azure の予算に対する支出をプログラムによって表示することもできます。
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

クラウドソリューションプロバイダー (CSP) パートナーは、パートナーセンター Api を使用して Azure の支出を表示および管理できます。 また、Azure の支出予算に対する顧客の支出をプログラムによって表示することもできます。

詳細については、「 [CSP パートナーがパートナーセンター api を使用して顧客とパートナーのアカウントおよび注文を管理するシナリオ](scenarios.md)」、特に「[背景」セクション](scenarios.md#background)を参照してください。

## <a name="partner-usage-management"></a>パートナーの使用状況管理

- **PartnerUsageSummary**リソースを使用して[パートナーの使用状況の概要を取得する](get-a-partner-usage-summary.md)
- **CustomerMonthlyUsageRecord**リソースを使用する[すべてのお客様の使用状況レコードを取得](get-a-customer-s-usage-records.md)する

## <a name="customer-usage-management"></a>顧客の使用状況管理

- **CustomerUsageSummary**リソースを使用して[顧客の使用状況の概要を取得する](get-a-customer-usage-summary.md)
- **SubscriptionMonthlyUsageRecord**リソースを使用して[顧客のすべてのサブスクリプション使用状況レコードを取得](get-a-customer-subscription-s-usage-records.md)する

## <a name="subscription-usage-management"></a>サブスクリプションの使用状況管理

- **SubscriptionUsageSummary**リソースを使用して[サブスクリプションの使用状況の概要を取得する](get-a-customer-subscription-usage-summary.md)
- **AzureResourceMonthlyUsageRecord**リソースを使用して[、サブスクリプションの毎月の使用状況レコードをすべて取得](get-all-monthly-usage-records-for-a-subscription.md)します。
- **ResourceUsageRecord**リソースを使用して、[リソースによってサブスクリプションの使用状況データを取得](get-a-customer-subscription-resource-usage-records.md)する
- **MeterUsageRecord**リソースを使用して、[メーターでサブスクリプションの使用状況データを取得](get-a-customer-subscription-meter-usage-records.md)する

## <a name="azure-spending-budget-management"></a>Azure の支出予算管理

- **CustomerUsageSummary**リソースを使用して[顧客の使用量の予算を取得する](get-a-customer-s-usage-spending-budget.md)
- **CustomerUsageSummary**リソースを使用して[顧客の使用量の予算を更新する](update-a-customer-s-usage-spending-budget.md)
