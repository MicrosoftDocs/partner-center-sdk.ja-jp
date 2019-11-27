---
title: お客様の使用リソース
description: 使用量ベースのサブスクリプションと毎月の使用量 (CustomerMonthlyUsageRecord、CustomerUsageSummary、PartnerUsageSummary、SpendingBudget を含む) をお持ちのお客様向けのリソース。
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
# <a name="customer-usage-resources"></a>お客様の使用リソース

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

使用量ベースのサブスクリプションをお持ちのお客様には、月々の使用予算がある場合があります。 この予算では、顧客の最大使用量に制限を設定し、パートナーが時間の経過と共に使用状況を追跡できるようにします。

> [!NOTE]
> お客様の使用量番号は推定値であり、請求目的では使用できません。

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord**は、現在の月の顧客の使用量の推定金銭的コストを表します。

| プロパティ         | 種類               | 説明                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| 割り当て           | SpendingBudget     | 顧客に割り当てられた支出予算。                          |
| PercentUsed      | decimal             | 割り当てられた予算から使用された割合。                        |
| ResourceId       | string             | リソースの一意の識別子。                                   |
| ResourceName     | string             | リソースの名前。                                                |
| TotalCost        | decimal             | サブスクリプション内のリソースの総使用コストの推定値。|
| CurrencyLocale   | string             | 顧客の通貨のロケール。 Microsoft Azure (0145P) サブスクリプションで使用できます。            |
| CurrencyCode     | string             | 通貨コードを取得または設定します。 Azure プランで使用できます。           |
| USDTotalCost     | decimal             | 推定合計コストを USD で取得または設定します。 Azure プランで使用できます。                                         |
| IsUpgraded       | bool             | 顧客の Azure サブスクリプションがアップグレードされているかどうかを示す値を取得または設定します。 値**true**は、Azure プランを持つ顧客を表します。                         |
| LastModifiedDate | date               | 使用状況データが最後に変更された日付。                               |
| 属性       | ResourceAttributes | 使用状況レコードに対応するメタデータ属性。               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary**は、請求期間全体における顧客の使用状況の概要を表します。

| プロパティ         | 種類               | 説明                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| 割り当て           | SpendingBudget     | 顧客に割り当てられた支出予算。                                                                  |
| ResourceId       | string             | リソースの一意の識別子。 CustomerMonthlyUsageRecord のコンテキストでは、この id は顧客 id です。 |
| ResourceName     | string             | リソースの名前。 CustomerMonthlyUsageRecord のコンテキストでは、これは顧客名です。               |
| /日 | date               | 現在の請求期間の開始日。                                                                    |
| すべての日付   | date               | 現在の請求期間の終了日。                                                                      |
| TotalCost        | decimal             | サブスクリプション内のリソースの総使用コストの推定値。                                         |
| CurrencyLocale   | string             | 顧客の通貨のロケール。 Microsoft Azure (0145P) サブスクリプションで使用できます。                                         |
| CurrencyCode     | string             | 通貨コードを取得または設定します。 Azure プランで使用できます。                                         |
| USDTotalCost     | decimal             | 推定合計コストを USD で取得または設定します。 Azure プランサブスクリプションリソースで使用できます。                                         |
| LastModifiedDate | date               | 使用状況データが最後に変更された日付。                                                                       |
| Links            | ResourceLinks      | 使用状況の概要に対応するリソースリンク。                                                           |
| 属性       | ResourceAttributes | 使用状況の概要に対応するメタデータ属性。                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary**は、すべての顧客の使用量の予算を示すパートナーレベルの概要を表します。

| プロパティ         | 種類               | 説明                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | 文字列の配列   | 通知用の電子メールアドレスの一覧。                                                                   |
| 顧客の超過コスト | 整数          | 予算を超過している顧客の数。                                                                    |
| CustomersTrendingOver | 整数       | 予算を超過している顧客の数。                                                     |
| 顧客の Swithon のサブスクリプション  | 整数 | 使用量ベースのサブスクリプションを使用している顧客の数。                                               |
| ResourceId       | string             | リソースの一意の識別子。 CustomerMonthlyUsageRecord のコンテキストでは、この id は顧客 id です。 |
| ResourceName     | string             | リソースの名前。 CustomerMonthlyUsageRecord のコンテキストでは、これは顧客名です。               |
| /日 | date               | 現在の請求期間の開始日。                                                                    |
| すべての日付   | date               | 現在の請求期間の終了日。                                                                      |
| TotalCost        | decimal             | 請求期間の開始時点からの現在の使用状況に基づいて、すべての顧客使用量の推定総コスト。      |
| CurrencyLocale   | string             | 通貨のロケール。                                                                                             |
| LastModifiedDate | date               | 使用状況データが最後に変更された日付。                                                                       |
| Links            | ResourceLinks      | 使用状況の概要に対応するリソースリンク。                                                           |
| 属性       | ResourceAttributes | 使用状況の概要に対応するメタデータ属性。                                                      |

## <a name="spendingbudget"></a>SpendingBudget

**SpendingBudget**は、使用量ベースのサブスクリプションについて、この顧客に割り当てられた予算を表します。

| プロパティ   | 種類               | 説明                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| 金額     | decimal             | 割り当てられた予算。 値が null の場合、この顧客に割り当てられている支出予算はありません。 |
| 属性 | ResourceAttributes | 予算に対応するメタデータ属性。                                                |
