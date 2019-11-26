---
title: Offer resources
description: Describes a product listed in the reseller catalog that they can offer to their customers.
ms.assetid: 702B18DB-D78A-4E3B-BC8F-EFD4092131DE
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 287482a934fecd73bce7d455098b3ab8a39d527c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486892"
---
# <a name="offer-resources"></a>Offer resources

**Applies To**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Describes a product listed in the reseller catalog that they can offer to their customers.

## <a name="span-idofferspan-idofferspan-idofferoffer"></a><span id="Offer"/><span id="offer"/><span id="OFFER"/>Offer

| プロパティ                    | タスクバーの検索ボックスに                      | 説明                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | string                    | The offer identifier.                                                                                           |
| 名前                        | string                    | The offer name.                                                                                                 |
| 説明                 | string                    | A description of the offer.                                                                                     |
| minimumQuantity             | 整数                       | The minimum quantity available.                                                                                 |
| maximumQuantity             | 整数                       | The maximum quantity available.                                                                                 |
| rank                        | 整数                       | The offer rank or priority compared to other categories in the same product line. This property should be set only if there is more than one offer for a given product line.  |
| uri                         | string                    | The offer URI.                                                                                                  |
| locale                      | string                    | The locale in which the offer applies.                                                                          |
| country                     | string                    | The country/region  where the offer applies.                                                                    |
| category                    | [OfferCategory](#offercategory)           | The category of the offer.                                                                   |
| limitUnitOfMeasure          | string                    | A value that indicates the type of purchase limitation. 表示される値は次のとおりです。<br/> "None" - There are no restrictions on the number of subscriptions based on the offer purchased.<br/> "Concurrent" - The number of subscriptions that can exist on the customer tenant at a given time, this includes subscriptions that are active or canceled. This value applies mostly to small business offers where license counts are less than 300. De-provisionioned subscriptions don't count.<br/> "LifeTime" - The number of subscriptions that can exist for the lifetime of the customer tenant. This value is most applicable to Trials. De-provisionioned subscriptions don't count.      |
| limit                       | 整数                       | The amount of subscriptions that can be purchased of this offer based on the limitUnitOfMeasure.                |
| prerequisiteOffers          | string                    | The prerequisite offers.                                                                                        |
| isAddOn                     | boolean                   | A value indicating whether this instance is an addon.                                                           |
| hasAddOns                   | boolean                   | A value indicating whether this offer has any addons.                                                           |
| isAvailableForPurchase      | boolean                   | A value indicating whether this instance is available for purchase.                                             |
| 請求                     | string                    | Specifies the billing type for the line item purchase: "none", "usage", or "license".                           |
| supportedBillingCycles      | 文字列の配列          | Indicates the billing cycles supported for this offer. Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype)   |
| isAutoRenewable             | boolean                   | A value indicating whether the offer renews automatically.                                                      |
| upgradeTargetOffers         | 文字列の配列          | The list of offers that this offer can be upgraded to.                                                          |
| conversionTargetOffers      | 文字列の配列          | The list of offers that this offer can be converted to.                                                         |
| reselleeQualifications      | 文字列の配列          | The qualifications required by the customer in order for a partner to purchase the offer for that customer.     |
| resellerQualifications      | 文字列の配列          | The qualifications required by the partner in order to purchase the offer for a customer.                       |
| salesGroupId                | string                    | A string used to group offers into separate orders.                                                             |
| isTrial                     | boolean                   | A value indicating whether this is a trial offer.                                                               |
| product                     | [OfferProduct](#offerproduct)           | Gets the offer product.                                                                           |
| unitType                    | string                    | The type of the unit.                                                                                      |
| links                       | [OfferLinks](#offerlinks)               | The offer's "learn more" link.                                                                    |
| 属性                  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the offer.                         |

## <a name="span-idoffercategoryspan-idoffercategoryspan-idoffercategoryoffercategory"></a><span id="OfferCategory"/><span id="offercategory"/><span id="OFFERCATEGORY"/>OfferCategory

Describes the categorization of an offer. This includes the rank or priority of this offer category compared to others in the same product line.

| プロパティ   | タスクバーの検索ボックスに                                                           | 説明                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | string                                                         | The category identifier.                                                                                                                                                   |
| 名前       | string                                                         | The category name.                                                                                                                                                         |
| rank       | 整数                                                            | The category rank or priority compared to other categories in the same offer. This property should be set only if there is more than one offer category for a given offer. |
| locale     | string                                                         | The locale in which the offer applies.                                                                                                                        |
| country    | string                                                         | The country/region where the offer applies.                                                                                                                   |
| links      | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the OfferCategory.                                                                                                                     |
| 属性 | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the OfferCategory.                                                                                                                |

## <a name="span-idofferlinksspan-idofferlinksspan-idofferlinksofferlinks"></a><span id="OfferLinks"/><span id="offerlinks"/><span id="OFFERLINKS"/>OfferLinks

Contains links for learning more information about the offer.

| プロパティ  | タスクバーの検索ボックスに | 説明                 |
|-----------|------|-----------------------------|
| learnMore | [リンク] | The "learn more" link.      |
| self      | [リンク] | The self URI                |
| 次へ      | [リンク] | The next page of items.     |
| previous  | [リンク] | The previous page of items. |

## <a name="span-idofferproductspan-idofferproductspan-idofferproductofferproduct"></a><span id="OfferProduct"/><span id="offerproduct"/><span id="OFFERPRODUCT"/>OfferProduct

A product or service which may have more than one offer associated with it, each with different sets of features and targeted at different customer needs.

| プロパティ | タスクバーの検索ボックスに   | 説明              |
|----------|--------|--------------------------|
| Id       | string | The category identifier. |
| 名前     | string | The category name.       |
| Unit     | string | The product unit.        |
