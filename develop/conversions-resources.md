---
title: 変換に関するリソース
description: 変換リソースでは、試用版サブスクリプションから有料サブスクリプションへの変換がサポートされます。
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 10526af03ee66b81d790816dfa9925c28e410114
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096386"
---
# <a name="conversions-resources"></a>変換に関するリソース

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

変換リソースでは、試用版サブスクリプションから有料サブスクリプションへの変換がサポートされます。

## <a name="conversion"></a>変換

試用版のサブスクリプションを有料サブスクリプションに変換するために使用する情報が含まれています。

| プロパティ | Type | 説明 |
| -------- | ---- | ----------- |
| offerId | string | 元の試用版プランのプラン id。 |
| targetOfferId | string | ターゲットプランのプラン識別子。 |
| orderId | string | 順序識別子。 |
| 数量 | INT | ライセンスの数。 既定値は、試用版サブスクリプションのライセンス数です。 |
| billingCycle | string | パートナーがサブスクリプションに対して課金される頻度を示します。 使用可能な値:**毎月**(パートナーは月単位)、**年間**(パートナーは毎年請求)、または**なし**(パートナーには課金されません)。 試用版のサブスクリプションで使用されます)。 |

## <a name="conversionerror"></a>ConversionError

変換中に発生したエラーを表します。

| プロパティ | Type | 説明 |
| -------- | ---- | ----------- |
| code | string | 問題に関連付けられているエラーコード。 使用可能な値: **Other** (一般エラー)、 **ConversionsNotFound** (変換先の評価版サブスクリプションの変換が見つかりません)。
| description | string | 問題を説明するフレンドリテキスト。 |

## <a name="conversionresult"></a>ConversionResult

サブスクリプション変換の実行結果を表します。

| プロパティ       | Type                                | 説明                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | string                              | サブスクリプションの識別子です。                                           |
| offerId        | string                              | 元のプラン識別子。                                         |
| targetOfferId  | string                              | ターゲットプランのプラン識別子。                             |
| エラー          | [ConversionError](#conversionerror) | 変換の試行中にエラーが発生しました (該当する場合)。 |