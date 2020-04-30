---
title: サブスクリプションの利用状況に関するリソース
description: サブスクリプションの使用状況に関するリソースでは、使用量ベースの課金によるサブスクリプションについて説明します。 これらのサブスクリプションには、日単位および月単位の使用状況レコードと、各支払い期間の使用状況の概要が含まれています。
ms.assetid: 61B98AB8-D802-4EC1-91FB-B7A2B95DE20C
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: b5317596f8fe77e06aabcda98268186550e7c355
ms.sourcegitcommit: 59ac8346af04aa34f5d342002909d0b203654bfe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81666094"
---
# <a name="subscription-usage-resources"></a>サブスクリプションの利用状況に関するリソース

**適用対象:**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

次のサブスクリプション使用状況リソースを使用して、使用量ベースの課金で特定のサブスクリプションの使用状況に関する情報を取得できます。 これらのサブスクリプションには、日単位および月単位の使用状況レコードと、各支払い期間の使用状況の概要が含まれています。

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

***SubscriptionDailyUsageRecord**リソースは互換性のために残されており、不正確な結果が生成される可能性があります。「 [Azure の顧客の使用状況レコードを取得](get-a-customer-s-utilization-record-for-azure.md)する」で説明されている api を使用するようにアプリケーションを更新し、代わりに[Microsoft Azure の価格を取得](get-prices-for-microsoft-azure.md)することをお勧めします。*

**SubscriptionDailyUsageRecord**リソースは、1日に使用されるサブスクリプションの量を示します。

| プロパティ         | Type               | 説明                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| 使用された日付         | string             | サブスクリプションが使用された日 (日付/時刻形式)。                                 |
| ResourceId       | string             | GUID。 リソースの一意の ID。                                                          |
| ResourceName     | string             | リソースの名前。                                                                     |
| TotalCost        | decimal             | 指定した日にサブスクリプション内のリソースを使用した場合の推定総コスト。     |
| CurrencyLocale   | string             | サブスクリプションが使用されたロケールによって、請求書で使用する通貨が決まります。 |
| LastModifiedDate | string             | このレコードが最後に変更された日 (日付/時刻形式)。                             |
| 属性       | ResourceAttributes | リソースに対応するメタデータ属性。                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

**SubscriptionMonthlyUsageRecord**リソースは、1か月に使用されるサブスクリプションの量を示します。

| プロパティ         | Type               | 説明                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Status           | string             | サブスクリプションの状態: "none"、"active"、"中断"、または "deleted"。                  |
| PartnerOnRecord  | string             | "レコード上のパートナーの MPN ID"                                                        |
| OfferId          | string             | GUID。 このサブスクリプションに関連付けられているオファーの id。                                       |
| Id               | string             | GUID。 サブスクリプションまたはリソースの id。                                                 |
| 名前             | string             | サブスクリプションまたはリソースの名前。                                                     |
| TotalCost        | decimal             | 指定した月にサブスクリプション内のリソースを使用した場合の推定総コスト。   |
| CurrencyLocale   | string             | サブスクリプションが使用されたロケールによって、請求書で使用する通貨が決まります。 Microsoft Azure (0145P) サブスクリプションで使用できます。 |
| CurrencyCode     | string             | 通貨コードを取得または設定します。 Azure プランサブスクリプションリソースで使用できます。                                         |
| USDTotalCost     | decimal             | 推定合計コストを USD で取得または設定します。 Azure プランで使用できます。                                         |
| LastModifiedDate | string             | このレコードが最後に変更された日 (日付/時刻形式)。                             |
| 属性       | ResourceAttributes | リソースに対応するメタデータ属性。                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

**SubscriptionUsageSummary**リソースは、現在の請求期間内に特定のサブスクリプションが使用された量を示します。

| プロパティ         | Type               | 説明                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | string             | GUID。 サブスクリプションまたはリソースの id。 CustomerMonthlyUsageRecord のコンテキストでは、この id は顧客 id です。 |
| ResourceName     | string             | サブスクリプションまたはリソースの名前。 CustomerMonthlyUsageRecord のコンテキストでは、この名前は顧客名です。 |
| /日 | date               | 現在の請求期間の開始日 (日付と時刻の形式)。                                                     |
| すべての日付   | date               | 現在の請求期間の終了日 (日付/時刻形式)。                                                       |
| TotalCost        | double             | 指定した請求期間中にサブスクリプション内のリソースを使用した場合の推定総コスト。               |
| CurrencyLocale   | string             | サブスクリプションが使用されたロケールによって、請求書で使用する通貨が決まります。 Microsoft Azure (0145P) サブスクリプションで使用できます。 |
| CurrencyCode   | string             | 通貨コードを取得または設定します。 Azure プランで使用できます。                                         |
| USDTotalCost   | decimal             | 推定合計コストを USD で取得または設定します。 Azure プランサブスクリプションリソースで使用できます。                                         |
| LastModifiedDate | string             | このレコードが最後に変更された日 (日付/時刻形式)。                                                      |
| リンク            | ResourceLinks      | SubscriptionUsageSummary に対応するリソースリンク。                                                      |
| 属性       | ResourceAttributes | SubscriptionUsageSummary に対応するメタデータ属性。                                                 |
