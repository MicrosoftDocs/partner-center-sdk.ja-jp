---
title: プランリソース
description: リセラーのカタログに記載されている製品を顧客に提供することができます。
ms.assetid: 702B18DB-D78A-4E3B-BC8F-EFD4092131DE
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: a4bec5d83faa4454857cd093bb109495bce4c17a
ms.sourcegitcommit: bea0d0cf3c1af7a75c9b150d53de53193a673fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82118658"
---
# <a name="offer-resources"></a>プランリソース

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

リセラーのカタログに記載されている製品を顧客に提供することができます。

## <a name="offer"></a>プラン

| プロパティ                    | Type                      | 説明                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | string                    | プラン ID。                                                                                           |
| name                        | string                    | プラン名。                                                                                                 |
| description                 | string                    | プランの説明。                                                                                     |
| minimumQuantity             | INT                       | 使用可能な最小数量。                                                                                 |
| maximumQuantity             | INT                       | 利用可能な最大数量。                                                                                 |
| rank                        | INT                       | 同じ製品ライン内の他のカテゴリと比較したプランのランクまたは優先順位。 このプロパティは、特定の製品ラインに対して複数のプランがある場合にのみ設定する必要があります。  |
| uri                         | string                    | プランの URI。                                                                                                  |
| locale                      | string                    | プランが適用されるロケール。                                                                          |
| country                     | string                    | プランが適用される国/地域。                                                                    |
| category                    | [OfferCategory](#offercategory)           | オファーのカテゴリ。                                                                   |
| limitUnitOfMeasure          | string                    | 購入制限の種類を示す値です。 指定できる値は、次のとおりです。<br/> "なし"-購入したプランに基づくサブスクリプションの数に制限はありません。<br/> "同時実行"-特定の時点で顧客のテナントに存在できるサブスクリプションの数。これには、アクティブまたは取り消されたサブスクリプションが含まれます。 この値は、ほとんどの場合、ライセンス数が300未満の小規模ビジネスプランに適用されます。 Provisionioned サブスクリプションはカウントされません。<br/> "有効期間"-顧客テナントの有効期間中に存在できるサブスクリプションの数。 この値は、試用版に最も適しています。 Provisionioned サブスクリプションはカウントされません。      |
| limit                       | INT                       | LimitUnitOfMeasure に基づいて、このプランの購入可能なサブスクリプションの量。                |
| prerequisiteOffers          | string                    | 前提条件の提供。                                                                                        |
| isAddOn                     | boolean                   | このインスタンスがアドオンであるかどうかを示す値。                                                           |
| hasAddOns                   | boolean                   | このプランにアドオンがあるかどうかを示す値。                                                           |
| Isの購入      | boolean                   | このインスタンスを購入できるかどうかを示す値。                                             |
| 請求                     | string                    | 品目の購入の課金の種類を指定します: "none"、"usage"、または "license"。                           |
| supportedBillingCycles      | 文字列の配列          | このプランでサポートされている請求サイクルを示します。 サポートされている値は、 [BillingCycleType](product-resources.md#billingcycletype)で見つかったメンバー名です。   |
| isAutoRenewable             | boolean                   | オファーが自動的に更新されるかどうかを示す値。                                                      |
| upgradeTargetOffers         | 文字列の配列          | このプランをにアップグレードできるプランの一覧。                                                          |
| conversionTargetOffers      | 文字列の配列          | このオファーを変換できるプランの一覧。                                                         |
| reselleeQualifications      | 文字列の配列          | パートナーがその顧客のオファーを購入するために必要な資格。     |
| resellerQualifications      | 文字列の配列          | パートナーが顧客のオファーを購入するために必要な資格。                       |
| salesGroupId                | string                    | プランを別の注文にグループ化するために使用される文字列。                                                             |
| isTrial                     | boolean                   | 評価版であるかどうかを示す値です。                                                               |
| product                     | [OfferProduct](#offerproduct)           | オファー製品を取得します。                                                                           |
| unitType                    | string                    | 単位の型。                                                                                      |
| リンク                       | [OfferLinks](#offerlinks)               | プランの "詳細情報" リンク。                                                                    |
| attributes                  | [ResourceAttributes](utility-resources.md#resourceattributes) | オファーに対応するメタデータ属性。                         |

## <a name="offercategory"></a>OfferCategory

オファーの分類について説明します。 これには、同じ製品ライン内の他のカテゴリと比較した、このオファーカテゴリのランクまたは優先順位が含まれます。

| プロパティ   | Type                                                           | 説明                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | string                                                         | カテゴリ識別子。                                                                                                                                                   |
| name       | string                                                         | カテゴリ名。                                                                                                                                                         |
| rank       | INT                                                            | 同じプラン内の他のカテゴリと比較したカテゴリのランクまたは優先順位。 このプロパティは、特定のプランに対して複数のプランカテゴリがある場合にのみ設定する必要があります。 |
| locale     | string                                                         | プランが適用されるロケール。                                                                                                                        |
| country    | string                                                         | プランが適用される国/地域。                                                                                                                   |
| リンク      | [ResourceLinks](utility-resources.md#resourcelinks)           | OfferCategory に対応するリソースリンク。                                                                                                                     |
| attributes | [ResourceAttributes](utility-resources.md#resourceattributes) | OfferCategory に対応するメタデータ属性。                                                                                                                |

## <a name="offerlinks"></a>OfferLinks

プランに関する詳細情報を提供するリンクが含まれています。

| プロパティ  | Type | 説明                 |
|-----------|------|-----------------------------|
| learnMore | Link | [詳細情報] リンク      |
| 自身      | Link | 自己 URI                |
| [次へ]      | Link | 項目の次のページ。     |
| previous  | Link | 項目の前のページ。 |

## <a name="offerproduct"></a>OfferProduct

製品またはサービスに複数のプランが関連付けられており、それぞれに異なる機能セットがあり、顧客のニーズが異なる場合があります。

| プロパティ | Type   | 説明              |
|----------|--------|--------------------------|
| Id       | string | カテゴリ識別子。 |
| 名前     | string | カテゴリ名。       |
| ユニット     | string | 製品単位。        |
