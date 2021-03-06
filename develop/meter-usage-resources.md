---
title: メーター使用状況レコードリソース
description: MeterUsageRecord リソースを使用して、現在の請求サイクルにおけるサブスクリプションのメータリングレベルの使用量の推定金銭的コストを示すことができます。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c02c859d1d8ba3edd236d83d3056cb82533f7e8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094771"
---
# <a name="meter-usage-record-resource"></a>メーター使用状況レコードリソース

**適用対象:**

- パートナー センター

**MeterUsageRecord**リソースを使用して、現在の請求サイクルにおけるサブスクリプションのメータリングレベルの使用量の推定金銭的コストを示すことができます。

## <a name="meterusagerecord"></a>MeterUsageRecord

| プロパティ         | Type               | 説明                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | パートナーセンターの[サブスクリプションリソース](subscription-resources.md#subscription)の識別子に対応する GUID。これは、Microsoft Azure (0145P) サブスクリプションまたは Azure プランを表します。 Microsoft Azure (0145P) サブスクリプションの場合、この値はコマースサブスクリプション識別子です。 Azure プランのサブスクリプションリソースの場合、この値は Azure プランの識別子です。                  |
| MeterId  | string             | メーター識別子を取得または設定します。                                                        |
| MeterName          | string             | メーターの名前を取得または設定します。                                       |
| カテゴリ               | string             | Azure リソースカテゴリを取得または設定します。                                                 |
| サブカテゴリ             | string             |  Azure リソースのサブカテゴリを取得または設定します。                                                     |
| QuantityUsed        | decimal             | Azure リソースの使用量を取得または設定します。   |
| ユニット   | string             | Azure リソースの長さの単位を取得または設定します。 |
| TotalCost   | decimal             | 使用率の推定総コストを取得または設定します。 |
| CurrencyLocale   | string             | サブスクリプションが使用されたロケール。 このプロパティは、請求書で使用される通貨を決定します。 このプロパティは、Microsoft Azure (0145P) サブスクリプションで使用できます。 |
| CurrencyCode   | string             | 通貨コードを取得または設定します。 このプロパティは、Azure プランで使用できます。                                         |
| USDTotalCost   | decimal             | 推定合計コストを USD で取得または設定します。 このプロパティは、Azure プランで使用できます。                                         |
| LastModifiedDate | string             | このレコードが最後に変更された日 (日付と時刻の形式)。                             |
| 属性       | ResourceAttributes | リソースに対応するメタデータ属性。                                        |                                           |
