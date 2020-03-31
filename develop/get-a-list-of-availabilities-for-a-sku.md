---
title: SKU に使用できる機能の一覧を取得する (国別)
description: 指定された製品および SKU の利用能力のコレクションを顧客の国別に取得する方法。
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: b8474506ecb928785c274566eda393ccd96620f4
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415621"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a>SKU に使用できる機能の一覧を取得する (国別)

適用対象

- Partner Center

このトピックでは、指定された製品および SKU の特定の国で利用できる機能のコレクションを取得する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 製品識別子。
- SKU 識別子。
- 国。

## <a name="c"></a>C\#

[SKU](product-resources.md#sku)に使用できる機能の一覧を取得するには、[次のよう](product-resources.md#availability)にします。

1. 「 [ID で sku を取得](get-a-sku-by-id.md)する」の手順に従って、特定の sku の操作のインターフェイスを取得します。
2. SKU インターフェイスから、[利用**能力**] プロパティを選択して、利用できる操作を含むインターフェイスを取得します。
3. Optional**Bytargetsegment ()** メソッドを使用して、ターゲットセグメントで可用性をフィルター処理します。
4. **Get ()** または**GetAsync ()** を呼び出して、この SKU の利用能力のコレクションを取得します。

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string targetSegment;
string productIdForAzureReservation;
string skuIdForAzureReservation;

// Get the availabilities.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.Get();

// Get the availabilities, filtered by target segment.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.BySegment(targetSegment).Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.ByReservationScope("AzurePlan").Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Azure plans only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.Get();

```

## <a name="rest"></a>REST

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求の構文

| メソッド  | 要求 URI                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities? country = {country-code} & targetsegment = {target-SEGMENT} HTTP/1.1     |

#### <a name="uri-parameters"></a>URI パラメーター

SKU に利用できる機能の一覧を取得するには、次のパスとクエリパラメーターを使用します。

| Name                   | 種類     | 必須 | 説明                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| 製品 id             | string   | はい      | 製品を識別する文字列。                           |
| sku-id                 | string   | はい      | SKU を識別する文字列。                               |
| 国-コード           | string   | はい      | 国/地域 ID。                                            |
| ターゲット-セグメント         | string   | いいえ       | フィルター処理に使用するターゲットセグメントを識別する文字列。 |
| reservationScope | string   | いいえ | Azure 予約 SKU の利用可能な機能の一覧を照会するときに、`reservationScope=AzurePlan` を指定して、AzurePlan に適用できる利用可能な機能の一覧を取得します。 Microsoft Azure (0145P) サブスクリプションに適用できる利用可能な機能の一覧を取得するには、このパラメーターを除外します。  |

#### <a name="request-headers"></a>要求ヘッダー

詳細については、「[ヘッダー](headers.md)」を参照してください。

#### <a name="request-body"></a>[要求本文]

[なし]。

#### <a name="request-examples"></a>要求の例

##### <a name="availabilities-for-sku-by-country"></a>国別の SKU の利用能力

次の例に従って、特定の SKU の利用できる機能の一覧を国別に取得します。

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

##### <a name="availabilities-for-vm-reservations-azure-plan"></a>VM 予約の利用能力 (Azure プラン)

次の例に従って、Azure VM 予約 Sku の国別利用できる機能の一覧を取得します。 この例は、Azure プランに適用される Sku を対象としています。

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

##### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure (MS AZR-0145P) サブスクリプションの VM 予約の可用性機能

次の例に従って、Microsoft Azure (0145P) サブスクリプションに適用される Azure VM 予約の国別の利用可能な機能の一覧を取得します。

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

### <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[**可用性**](product-resources.md#availability)リソースのコレクションが含まれます。

#### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

このメソッドは、次のエラーコードを返します。

| HTTP 状態コード     | エラー コード   | 説明                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | 要求された**Targetsegment**へのアクセスは許可されていません。                                                     |

#### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02,70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllcw==?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:37 GMT
Content-Length: 808

{
    "totalCount": 1,
    "items": [
        {
            "id": "DZH318XZXVNF",
            "productId": "DZH318Z0BQ3Q",
            "skuId": "0001",
            "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXVNF",
            "defaultCurrency": {
                "code": "USD",
                "symbol": "$"
            },
            "segment": "commercial",
            "country": "US",
            "isPurchasable": true,
            "isRenewable": false,
            "terms": [{
                "duration": "P1Y",
                "description": "1 Year Prepaid"
            }],
            "product": { ... },
            "sku": { ... },
            "links": {
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318Z0HMKQ?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetSegment=commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
