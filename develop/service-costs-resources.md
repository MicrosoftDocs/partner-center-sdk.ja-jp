---
title: サービスコストリソース
description: 顧客が購入したサービスに関連するリソースについて説明します。
ms.assetid: 2916B7F3-06D5-4DC1-A137-CD8270258CDB
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e61ef7e2d6c72938a365d28774a90b993c5d3e7b
ms.sourcegitcommit: 59ac8346af04aa34f5d342002909d0b203654bfe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81666304"
---
# <a name="service-costs-resources"></a>サービスコストリソース

**適用対象:**

- パートナー センター

顧客が購入したサービスに関連するリソースについて説明します。

## <a name="servicecostssummary"></a>ServiceCostsSummary

**ServiceCostsSummary**には、請求期間中に、指定した顧客によって購入されたすべてのサービスを集計する概要が含まれています。

| プロパティ | Type | 説明 |
| -------- | ---- | ----------- |
| details | [ServiceCostsSummaryDetail](#servicecostssummarydetail)オブジェクトの配列 | 請求書の種類別に識別されるサービスコストの概要の詳細一覧。|
| リンク | [ResourceLinks](utility-resources.md#resourcelinks) | リソースリンク。 |
| attributes | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。 |

> [!IMPORTANT]
> **次の表のフィールドは非推奨とされます。** 定期的および1回限りのサービスコストの概要を取得するには、代わりに [**詳細**] フィールドを使用します。 **詳細**フィールドは、前の表で説明されています。 **詳細**フィールドの対応するデータ値を参照しますが、ルートレベルのフィールドは参照しません。

| プロパティ | Type | 説明 |
| -------- | ---- | ----------- |
| /日 | date | 請求期間の開始日。 |
| すべての日付 | date | 請求期間の終了日。 |
| これは、合計 | double | 顧客のすべてのコストの課税前の合計。 |
| 税金  | double | 顧客によって購入されたすべての品目に発生した税金の合計。 |
| afterTaxTotal | double | 顧客が購入したすべての品目の総コスト。 |
| currencyCode | string | コストに使用する通貨を表します。 |
| currencySymbol | string | コストに使用される通貨記号。 |
| customerId | string | 購入を行っている顧客の ID。 |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**ServiceCostsSummaryDetail**は、請求期間中に指定した顧客によって購入されたすべてのサービス (定期的または1回限りの請求) を集計するサービスコストの概要を示します。

| プロパティ | Type | 説明 |
| -------- | ---- | ----------- |
| invoiceType | string | サービスコストの概要が生成された invoiceType。 |
| summary | [ServiceCostsSummary](#servicecostssummary) | 1つの請求書の種類で顧客によって集計されたサービスコストの概要。 |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**ServiceCostLineItem**は、顧客が購入した1つの項目について説明します。

> [!IMPORTANT]
> 次のプロパティは、製品が1回だけ*購入*されるサービスコスト明細項目 ( **productId**、 **productName**、 **skuId**、 **skuname**、 **availabilityId**、 **publisherId**、 **publishername**、 **termandbil**、 **discountdetails**)*にのみ適用*されます。 これらのプロパティは、製品が*定期的に購入*されるサービスライン項目には適用され*ません*。 たとえば、これらのプロパティは、サブスクリプションベースの Office 365 および Azure には適用され*ません*。

| プロパティ                 | Type                           | 説明                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| startDate                | UTC 日時形式の文字列 | 請求の開始日。                                       |
| endDate                  | UTC 日時形式の文字列 | 料金の終了日。                                         |
| subscriptionFriendlyName | string                         | サブスクリプションのフレンドリ名。                              |
| subscriptionId           | string                         | サブスクリプションの識別子です。                                         |
| orderId                  | string                         | 順序識別子。                                                |
| offerId                  | string                         | プラン ID。                                                |
| offerName                | string                         | プラン名。                                                      |
| resellerMPNId            | string                         | 2層のパートナーシナリオでのみ使用されます。 MPN 識別子を参照します。 |
| chargeType               | string                         | 関連付けられている料金の種類。                                          |
| 数量                 | number                         | 使用または購入したユニットの数量。                             |
| unitPrice                | number                         | ユニットあたりの料金。                                                  |
| これは、合計              | number                         | 税金までのこの品目の合計請求額。                         |
| 税金                      | number                         | この項目に対して発生した税金の合計金額。                         |
| afterTaxTotal            | number                         | このアイテムの総コスト。                                    |
| currencyCode             | string                         | コストに使用する通貨を表します。                          |
| currencySymbol           | string                         | コストに使用される通貨記号。                              |
| customerId               | string                         | 購入を行っている顧客の ID。                          |
| customerName             | string                         | 購入を行っている顧客の名前。                        |
| invoiceNumber            | string                         | この行項目が属する請求書番号。                   |
| productId                | string                         | 製品識別子。                                              |
| skuId                    | string                         | Sku 識別子。                                                  |
| availabilityId           | string                         | 可用性識別子。                                         |
| productName              | string                         | 製品名。                                                    |
| skuName                  | string                         | Sku の名前。                                                        |
| publisherName            | string                         | 発行元の名前。                                                  |
| publisherId              | string                         | パブリッシャーの識別子。                                            |
| Termandbilのサイクル      | string                         | 期間と請求サイクル。                                          |
| discountDetails          | string                         | 割引の詳細。                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| プロパティ             | Type                               | 説明                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [リンク](utility-resources.md#link) | 行項目を取得する URI。 |
| 自身                 | [リンク](utility-resources.md#link) | 自己 URI。                       |
