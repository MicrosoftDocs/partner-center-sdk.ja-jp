---
title: Azure 使用率レコードリソース
description: Azure 使用率レコードには、Azure サブスクリプションリソースの使用状況に関する詳細が含まれています。
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 21d39c4497c00f5abeeeb771dfe20cd1e2b1c13a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094564"
---
# <a name="azure-utilization-record-resources"></a>Azure 使用率レコードリソース

**適用対象:**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Azure 使用率レコードには、Azure サブスクリプションリソースの使用状況に関する詳細が含まれています。 お客様の Azure サブスクリプションの課金関係を所有しているクラウドサービスプロバイダーパートナーの方は、この REST API を使用して、各請求サイクルの終了時に請求書を顧客に送信するために、サブスクリプションで発生した使用量を追跡するためのスケーラブルな方法を提供できます。

使用量を追跡し、個々の顧客の毎月の請求書と請求額を予測できるようにするには、料金カードクエリを組み合わせて、 [Azure の顧客の使用状況レコードを取得](get-a-customer-s-utilization-record-for-azure.md)するための要求に[Microsoft Azure の価格を取得](get-prices-for-microsoft-azure.md)します。

価格は市場と通貨によって異なります。この API は、場所を考慮します。 既定では、API はパートナーセンターとブラウザーの言語でパートナーのプロファイル設定を使用します。これらの設定はカスタマイズできます。 拠点を認識することは、1つの集中管理されたオフィスから複数の市場で売上を管理する場合に特に重要です。

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Azure 使用率レコードリソースのプロパティについて説明します。

| プロパティ       | Type                                      | 必須 | 説明                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | string                                    | はい      | 使用状況集計の時間範囲の開始。 応答は、消費時間によってグループ化されます (リソースが実際に使用された時間と、課金システムに報告された日時)。 |
| usageEndTime   | string                                    | はい      | 使用状況集計の時間範囲の最後。 応答は、消費時間によってグループ化されます。 つまり、リソースが実際に使用されたときと、が課金システムに報告された日時です。   |
| resource       | object                                    | はい      | [Azureresource](#azureresource)オブジェクトが含まれています。                                                                                                                                     |
| 数量       | number                                    | はい      | [Azureresource](#azureresource)の消費量。                                                                                                                           |
| unit           | 文字列                                    | いいえ       | 数量の種類 (時間、バイトなど)このプロパティは省略可能です。                                                                                                                     |
| infoFields     | object                                    | はい      | インスタンスレベルの詳細のキーと値のペア。 このオブジェクトは空でもかまいません。                                                                                                                    |
| instanceData   | object                                    | いいえ       | インスタンスレベルの詳細のキーと値のペアを含む[Azureinstancedata](#azureinstancedata)オブジェクトを格納します。 このプロパティは省略可能であり、含めることはできません。                  |
| 属性     | [ResourceAttributes](utility-resources.md#resourceattributes) | はい      | メタデータ属性。 "ObjectType": "AzureUtilizationRecord" が含まれています。                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>AzureUtilizationRecord リソースに対する操作

- [Azure に関する顧客の使用率レコードを取得する](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>Remove-azureresource

Azure リソースのプロパティについて説明します。

| プロパティ    | Type   | 必須 | 説明                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | string | はい      | Azure リソースの一意識別子。 ResourceID またはリソース GUID とも呼ばれます。 |
| name        | 文字列 | いいえ       | 使用されているリソースのわかりやすい名前。 このプロパティは省略可能です。            |
| category    | string | いいえ       | 消費されたリソースのカテゴリ。 このプロパティは省略可能です。                   |
| サブカテゴリ | 文字列 | いいえ       | 消費されたリソースのサブカテゴリ。 このプロパティは省略可能です。               |
| region      | 文字列 | いいえ       | 消費されたリソースの領域。 このプロパティは省略可能です。                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Azure インスタンスデータリソースのプロパティについて説明します。

| プロパティ       | Type             | 必須 | 説明                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | string           | はい      | 完全修飾 Azure リソース ID。リソースグループとインスタンス名が含まれます。                   |
| location       | string           | はい      | サービスが実行されたリージョン。                                                                               |
| partNumber     | object           | はい      | コマーシャルマーケットプレースサードパーティの使用に関するリソースを識別するために使用される一意の名前空間。 このプロパティには、空の文字列を指定できます。 |
| orderNumber    | number           | はい      | 商用 marketplace のサードパーティ注文を識別するために使用される一意の名前空間。 このプロパティには、空の文字列を指定できます。          |
| tags           | 文字列の配列 | いいえ       | ユーザーによって指定されたリソースタグ。 このプロパティは省略可能であり、含めることはできません。                            |
| additionalInfo | 文字列の配列 | いいえ       | Azure リソースの追加データ。 このプロパティは省略可能であり、含めることはできません。                          |