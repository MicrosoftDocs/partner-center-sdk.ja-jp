---
title: ID で可用性を取得する
description: 可用性 ID を使用して、指定された製品と SKU の可用性を取得します。
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 824303d40e1dcb0405246c8e29562c4527d147fd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86093891"
---
# <a name="get-the-availability-by-id"></a>ID で可用性を取得する

**適用対象**

- パートナー センター

可用性 ID を使用して、指定された製品と SKU の可用性を取得します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 製品 ID。

- SKU ID。

- 可用性 ID。

## <a name="c"></a>C\#

特定の[可用性](product-resources.md#availability)の詳細を取得するには、まず「 [ID で sku を取得](get-a-sku-by-id.md)する」の手順に従って、特定の[sku の](product-resources.md#sku)操作のインターフェイスを取得します。 生成されたインターフェイスから使用可能なプロパティを選択し**て、利用**可能な操作を持つインターフェイスを取得します。 その後、可用性 ID を**ById ()** メソッドに渡して、その特定の可用性に対する操作を取得し、 **get ()** または**GetAsync ()** を呼び出して可用性の詳細を取得します。

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

特定の[可用性](product-resources.md#availability)の詳細を取得するには、まず「 [ID で sku を取得](get-a-sku-by-id.md)する」の手順に従って、特定の[sku の](product-resources.md#sku)操作のインターフェイスを取得します。 生成されたインターフェイスから、 **Getavailability アビリティー**関数を選択して、利用可能な操作を持つインターフェイスを取得します。 その後、可用性 ID を**byId ()** 関数に渡して、その特定の可用性に対する操作を取得し、 **get ()** 関数を呼び出して可用性の詳細を取得します。

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

特定の[可用性](product-resources.md#availability)の詳細を取得するには、 **AvailabilityId**、 **CountryCode**、 **ProductId**、および**SkuId**パラメーターを指定して、 [**get partnerproductavailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md)を実行し、可用性の詳細を取得します。

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}? country = {country-CODE} HTTP/1.1         |

### <a name="uri-parameter"></a>URI パラメーター

可用性 ID を使用して特定の可用性を取得するには、次のパスとクエリパラメーターを使用します。

| 名前                   | Type     | 必須 | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| 製品 id             | string   | はい      | 製品を識別する GUID 形式の文字列。            |
| sku-id                 | string   | はい      | SKU を識別する GUID 形式の文字列。                |
| 可用性-id        | string   | はい      | 可用性を識別する GUID 形式の文字列。       |
| 国-コード           | string   | はい      | 国/地域 ID。                                            |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[可用性](product-resources.md#availability)リソースが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

このメソッドは、次のエラーコードを返します。

| HTTP 状態コード     | エラー コード   | 説明                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | 製品が見つかりませんでした。                                                                                    |
| 404                  | 400018       | Sku が見つかりませんでした。                                                                                        |
| 404                  | 400019       | 可用性が見つかりません。                                                                                   |

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
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
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
