---
title: インベントリの確認
description: 特定のカタログ項目のセットの在庫を確認します。
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 347b131efccee318043c824984285fde9cd38a64
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488972"
---
# <a name="check-inventory"></a>インベントリの確認

適用対象:

- パートナー センター

特定のカタログアイテムのセットの在庫を確認する方法。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 1つまたは複数の製品 Id。 必要に応じて、SKU Id を指定することもできます。
- 指定された製品/SKU ID によって参照されている SKU のインベントリを確認するために必要な追加のコンテキスト。 これらの要件は、製品/SKU の種類によって異なる場合があり、 [sku の](product-resources.md#sku) **InventoryVariables**プロパティから決定できます。 

## <a name="c"></a>C#


インベントリを確認するには、チェックする項目ごとに[InventoryItem](product-resources.md#inventoryitem)オブジェクトを使用して[InventoryCheckRequest](product-resources.md#inventorycheckrequest)オブジェクトを作成します。 次に、 **iaggregatepartner.customers**アクセサーを使用して、**製品**にスコープを適用し、 **bycountry ()** メソッドを使用して国を選択します。 最後に、 **InventoryCheckRequest**オブジェクトを使用して**checkinventory ()** メソッドを呼び出します。

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string subscriptionId;
string countryCode;
string productId;

// Build the inventory check request details object.
var inventoryCheckRequest = new InventoryCheckRequest()
{
    TargetItems = new InventoryItem[]{ new InventoryItem { ProductId = productId } },
    InventoryContext = new Dictionary<string, string>()
    {
      { "customerId", customerId },
      { "azureSubscriptionId", subscriptionId }
      { "armRegionName", armRegionName }
    }
};

// Get the inventory results.
var inventoryResults = partnerOperations.Extensions.Product.ByCountry(countryCode).CheckInventory(inventoryCheckRequest);
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド   | 要求 URI                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **投稿** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/extensions/product/checkInventory? country = {country-CODE} HTTP/1.1                        |

### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを使用して、インベントリを確認します。

| 名前                   | 種類     | 必須 | 説明                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| 国-コード           | string   | 〇      | 国/地域 ID。                                            |

### <a name="request-headers"></a>要求ヘッダー

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

1つ以上の[InventoryItem](product-resources.md#inventoryitem)リソースを含む[InventoryCheckRequest](product-resources.md#inventorycheckrequest)リソースで構成される在庫要求の詳細。 

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/extensions/product/checkinventory?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json

{"TargetItems":[{"ProductId":"DZH318Z0BQ3P"}],"InventoryContext":{"customerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d","azureSubscriptionId":"3A231FBE-37FE-4410-93FD-730D3D5D4C75","armRegionName":"Europe"}}
```

## <a name="response"></a>応答

成功した場合、応答本文には、制限の詳細が設定されている[InventoryItem](product-resources.md#inventoryitem)オブジェクトのコレクションが含まれます (該当する場合)。

>[!NOTE]
>入力 InventoryItem がカタログに見つからなかった項目を表している場合、その項目は出力コレクションに含まれません。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

このメソッドは、次のエラーコードを返します。

| HTTP 状態コード     | エラー コード   | 説明                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 400                  | 2001         | 要求本文がありません。                                                                              |
| 400                  | 400026       | 必要なインベントリコンテキスト項目がありません。                                                             |

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 1021
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
X-Locale: en-US
[
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0039",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0038",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "000S",
        "isRestricted": false,
        "restrictions": []
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0011",
        "isRestricted": false,
        "restrictions": []
    }
]
```