---
title: Azure 料金カードのリソース
description: Azure 料金カードでは、Azure プランのリアルタイム料金が提供されます。
ms.assetid: A42B4FFA-278E-41FF-B51E-E48C2CA70EEF
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e81debb15c30ba024d897a00075bffe28be3acaf
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489142"
---
# <a name="azure-rate-card-resources"></a>Azure 料金カードのリソース

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Azure 料金カードでは、Azure プランのリアルタイム料金が提供されます。 Azure の価格は非常に動的で、頻繁に変更されます。 Microsoft はパートナーセンターで更新プログラムを発行しますが、REST API は、クラウドソリューションプロバイダーパートナーが現在の価格を取得するための最速の方法を提供します。

使用量を追跡し、個々の顧客の毎月の請求書と請求額を予測できるようにするには、料金カードクエリを組み合わせて、 [Azure の顧客の使用状況レコードを取得](get-a-customer-s-utilization-record-for-azure.md)するための要求に[Microsoft Azure の価格を取得](get-prices-for-microsoft-azure.md)します。

価格は市場と通貨によって異なります。この API は、場所を考慮します。 既定では、パートナーのプロファイル設定はパートナーセンターとブラウザーの言語で使用されますが、カスタマイズすることもできます。 これは、1つの集中管理されたオフィスから複数の市場で売上を管理する場合に特に関連します。

## <a name="azureratecard"></a>AzureRateCard

Azure 料金カードリソースのプロパティについて説明します。

| プロパティ      | 種類                                      | 説明                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| 貨      | string                                    | 料金が提供される通貨。                     |
| isTaxIncluded | boolean                                   | すべてのレートは税込みなので、常に "false" として返されます。 |
| locale        | string                                    | リソース情報がローカライズされるカルチャ。       |
| メーター        | オブジェクトの配列                          | [Azuremeter](#azuremeter)オブジェクトの配列。                       |
| offerTerms    | オブジェクトの配列                          | [AzureOfferTerm](#azureofferterm)オブジェクトの配列。               |
| 属性    | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。 "ObjectType": "AzureRateCard" が含まれています。   |


### <a name="operations-on-the-azureratecard-resource"></a>AzureRateCard リソースに対する操作

- [Microsoft Azure の価格を取得する](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| プロパティ         | 種類             | 説明                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | string           | メーターの一意の識別子。                                                                    |
| name             | string           | メーターのフレンドリ名。                                                                   |
| 料率            | オブジェクト           | メーターレート。 キーはメーターの数量 (文字列) で、値はメーターのレート (number) です。 |
| tags             | 文字列の配列 | 測定タグ (省略可能)。 この配列は空にすることができます。                                                 |
| 別         | string           | リソースのカテゴリ。                                                                     |
| サブカテゴリ      | string           | リソースのサブカテゴリ。                                                                 |
| 領域 (region)           | string           | Id のリージョン。                                                                             |
| ユニット             | string           | 数量の種類 (時間、バイトなど)                                                     |
| includedQuantity | number           | 無料で含まれているメーターの数量。                                               |
| effectiveDate    | string           | このメーターが有効な日付。                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| プロパティ         | 種類             | 説明                             |
|------------------|------------------|-----------------------------------------|
| name             | string           | プランの用語のフレンドリ名。        |
| 価格         | number           | 適用されている割引 (存在する場合)。           |
| excludedMeterIds | 文字列の配列 | プランから除外されたメーター (存在する場合)。 |
| effectiveDate    | string           | プランが有効である日付。        |