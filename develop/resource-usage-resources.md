---
title: リソース使用状況レコードリソース
description: ResourceUsageRecord リソースを使用して、現在の請求サイクルにおけるサブスクリプションのリソースレベルの使用量の推定金銭的コストを記述できます。
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2ec59df657a5b49209da9e801dcfcae4a3282d56
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488092"
---
# <a name="resource-usage-record-resources"></a>リソース使用状況レコードリソース

適用対象:

- パートナー センター

**ResourceUsageRecord**リソースを使用して、現在の請求サイクルにおけるサブスクリプションのリソースレベルの使用量の推定金銭的コストを記述できます。

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| プロパティ         | 種類               | 説明                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | サブスクリプション識別子を取得します。値の設定もできます。 Microsoft Azure (0145P) サブスクリプションの場合、この値はコマースサブスクリプション識別子です。 Azure プランの場合、この値は Azure プラン識別子です)。                  |
| resourceUri  | string             | リソース URI を取得または設定します。 "                                                        |
| ResourceType          | string             | リソースの種類を取得または設定します。                                       |
| EntitlementId               | string             | 権利識別子 (Azure サブスクリプション識別子) を取得または設定します。                                                 |
| EntitlementName             | string             | 権利の名前を取得または設定します。                                                     |
| ResourceGroupName        | double             | リソースグループ名を取得または設定します。   |
| 名前   | string             | リソースの名前。 |
| ResourceName   | string             | リソースの名前を取得または設定します。 |
| TotalCost   | decimal             | 推定総コスト使用量を取得します。値の設定もできます。 |
| CurrencyCode   | string             | 通貨コードを取得または設定します。                                          |
| USDTotalCost   | decimal             | 推定合計コストを USD で取得または設定します。                                         |
| LastModifiedDate | string             | このレコードが最後に変更された日 (日付と時刻の形式)。                             |
| 属性       | ResourceAttributes | リソースに対応するメタデータ属性。                                        |                                           |
