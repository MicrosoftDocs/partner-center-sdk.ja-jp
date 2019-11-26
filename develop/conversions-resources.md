---
title: Conversions resources
description: Conversion resources support the conversion of a trial subscription to a paid subscription.
ms.assetid: 4AE796E3-47D9-428B-8267-A5247B573E0C
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e91e79ce77ac020495c2d09a4bf33dd947231dec
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488902"
---
# <a name="conversions-resources"></a>Conversions resources

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Conversion resources support the conversion of a trial subscription to a paid subscription.

## <a name="conversion"></a>変換

Contains information used to convert a trial subscription to a paid subscription.

| プロパティ | タスクバーの検索ボックスに | 説明 |
| -------- | ---- | ----------- |
| offerId | string | The offer identifier of the original, trial offer. |
| targetOfferId | string | The offer identifier for the target offer. |
| orderId | string | The order identifier. |
| quantity | 整数 | The number of licenses. The default is the number of licenses in the trial subscription. |
| billingCycle | string | Indicates how often the partner is charged for the subscription. Possible values: **Monthly** (partner is billed monthly), **Annual** (partner is billed annually), or **None** (Partner isn't billed. Used for trial subscriptions). |

## <a name="conversionerror"></a>ConversionError

Represents an error that occurred during conversion.

| プロパティ | タスクバーの検索ボックスに | 説明 |
| -------- | ---- | ----------- |
| コード | string | The error code associated with the issue. Possible values: **Other** (general error), **ConversionsNotFound** (can't find any conversions for the trial subscription to convert to).
| 説明 | string | The friendly text describing the issue. |

## <a name="conversionresult"></a>ConversionResult

Represents the result of performing a subscription conversion.

| プロパティ       | タスクバーの検索ボックスに                                | 説明                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | string                              | The subscription identifier.                                           |
| offerId        | string                              | The original offer identifier.                                         |
| targetOfferId  | string                              | The offer identifier for the target offer.                             |
| エラーを修正する          | [ConversionError](#conversionerror) | The error encountered while attempting the conversion, if applicable.. |