---
title: Microsoft Azure の価格を取得する
description: Azure プランのリアルタイム価格で Azure 料金カードを取得する方法について説明します。 Azure の価格は非常に動的で、頻繁に変更されます。
ms.assetid: 65262585-0F3B-4BD0-83BE-B2695C33CDB7
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7aaa68d4a1eab5595d2325e84e555c3ec5117e08
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487312"
---
# <a name="get-prices-for-microsoft-azure"></a>Microsoft Azure の価格を取得する

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Azure プランのリアルタイム価格で[Azure 料金カード](azure-rate-card-resources.md)を取得する方法について説明します。 Azure の価格は非常に動的で、頻繁に変更されます。

使用量を追跡し、個々の顧客の毎月の請求書と請求額を予測するために、この Azure 料金カードクエリを組み合わせて、 [azure の顧客の使用状況レコードを取得](get-a-customer-s-utilization-record-for-azure.md)するための要求に関する Microsoft Azure の価格を取得することができます。

価格は市場と通貨によって異なります。この API は、場所を考慮します。 応答で返される通貨、地域、および言語をカスタマイズできます。 これは、1つの集中管理されたオフィスから複数の市場で売上を管理する場合に特に関連します。 詳細については、「 [URI パラメーター](#uri-parameters) 」を参照してください。 

## <a name="examples"></a>例

### <a name="c"></a>C#

Azure の料金カードを取得するには、 [**IAzureRateCard**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get)メソッドを呼び出して、azure の価格を含む[**AzureRateCard**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard)リソースを返します。

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: GetAzureRateCard.cs

### <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

Azure の料金カードを取得するには、 **IAzureRateCard**関数を呼び出して、azure の価格を含むレートカードの詳細を返します。

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

### <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

Azure カードを取得するには、 [**PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md)コマンドを実行して、azure 料金を含むレートカードの詳細を返します。

```powershell
Get-PartnerAzureRateCard
```

## <a name="request"></a>要求

### <a name="request-syntax"></a>要求の構文

| メソッド  | 要求 URI                                                        |
|---------|--------------------------------------------------------------------|
| **取得** | *{baseURL}* /v1/ratecards/azure? currency = {currency} & region = {region} |

### <a name="uri-parameters"></a>URI パラメーター

| 名前     | 種類   | 必須 | 説明                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 貨 | string | X       | リソースレートが提供される通貨に対して、省略可能な3文字の ISO コード (例: "EUR")。 既定値は "USD" です。 |
| 領域 (region)   | string | X       | プランが購入される市場を示す省略可能な2文字の ISO 国/地域コード (例: "FR")。 既定値は "US" です。        |

要求には、省略可能な X-Locale[ヘッダー](headers.md#request-headers)を含めることができます。 X-Locale ヘッダーを含めない場合は、既定値 ("en-us") が使用されます。
* 要求に currency および region パラメーターを指定する場合は、応答の言語を決定するために X ロケールの値が使用されます。
* 要求に地域と通貨のパラメーターを指定しない場合は、応答の地域、通貨、および言語を決定するために、X ロケールの値が使用されます。


### <a name="request-header"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="response"></a>応答


成功した場合は、 [Azure 料金カード](azure-rate-card-resources.md)リソースが返されます。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 1545508
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57b25659-fc00-4215-87e7-2b09bac6845d
MS-RequestId: 870118d0-adbb-41a3-82d2-a3d45ade3c73
MS-CV: CYBB8PXMsEukJBIn.0
MS-ServerId: 201021413
Date: Wed, 01 Feb 2017 00:13:45 GMT

{
    "locale": "en-US",
    "currency": "USD",
    "isTaxIncluded": false,
    "meters": [{
            "id": "4b836326-7e19-46e6-8bce-1b19bb6cd91e",
            "name": "Unlimited Data - 1 Gbps",
            "rates": {
                "0": 7395.0
            },
            "tags": [],
            "category": "Networking",
            "subcategory": "ExpressRoute",
            "region": "Zone 2",
            "unit": "Connections",
            "includedQuantity": 0.0,
            "effectiveDate": "2015-09-01T00:00:00Z"
        }, {
            "id": "1e8f6d9f-8b40-4c97-80cc-cff87a290a93",
            "name": "Compute Hours",
            "rates": {
                "0": 3.9729
            },
            "tags": [],
            "category": "Cloud Services",
            "subcategory": "Standard_L16 Cloud Services",
            "region": "AU East",
            "unit": "1 Hour",
            "includedQuantity": 0.0,
            "effectiveDate": "2016-09-01T00:00:00Z"
        }, {
            "id": "7a2639ce-ae47-4413-9837-6b4f4b78be3d",
            "name": "Compute Hours",
            "rates": {
                "0": 0.1122
            },
            "tags": [],
            "category": "Virtual Machines",
            "subcategory": "Standard_D1_v2 VM (Windows)",
            "region": "BR South",
            "unit": "Hours",
            "includedQuantity": 0.0,
            "effectiveDate": "2017-01-01T00:00:00Z"
        }
    ],
    "offerTerms": [{
            "name": "Overage discount",
            "discount": 0.15,
            "excludedMeterIds": ["53cc0061-0fe2-4249-bf62-e1008c811f5c", "c82dbd27-c978-43a7-ad41-525a90d8962b"],
            "effectiveDate": "2014-01-01T00:00:00"
        }
    ],
    "attributes": {
        "objectType": "AzureRateCard"
    }
}
```