---
title: 変換に関するリソース
description: 変換リソースでは、試用版サブスクリプションから有料サブスクリプションへの変換がサポートされます。
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
# <a name="conversions-resources"></a>変換に関するリソース

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

変換リソースでは、試用版サブスクリプションから有料サブスクリプションへの変換がサポートされます。

## <a name="conversion"></a>変換

試用版のサブスクリプションを有料サブスクリプションに変換するために使用する情報が含まれています。

| プロパティ | 種類 | 説明 |
| -------- | ---- | ----------- |
| offerId | string | 元の試用版プランのプラン id。 |
| targetOfferId | string | ターゲットプランのプラン識別子。 |
| orderId | string | 順序識別子。 |
| quantity | int | ライセンスの数。 既定値は、試用版サブスクリプションのライセンス数です。 |
| 周期サイクル | string | パートナーがサブスクリプションに対して課金される頻度を示します。 使用可能な値:**毎月**(パートナーは月単位)、**年間**(パートナーは毎年請求)、または**なし**(パートナーには課金されません)。 試用版のサブスクリプションで使用されます)。 |

## <a name="conversionerror"></a>ConversionError

変換中に発生したエラーを表します。

| プロパティ | 種類 | 説明 |
| -------- | ---- | ----------- |
| code | string | 問題に関連付けられているエラーコード。 使用可能な値: **Other** (一般エラー)、 **ConversionsNotFound** (変換先の評価版サブスクリプションの変換が見つかりません)。
| 説明 | string | 問題を説明するフレンドリテキスト。 |

## <a name="conversionresult"></a>ConversionResult

サブスクリプション変換の実行結果を表します。

| プロパティ       | 種類                                | 説明                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | string                              | サブスクリプション識別子。                                           |
| offerId        | string                              | 元のプラン識別子。                                         |
| targetOfferId  | string                              | ターゲットプランのプラン識別子。                             |
| error (エラー)          | [ConversionError](#conversionerror) | 変換の試行中にエラーが発生しました (該当する場合)。 |