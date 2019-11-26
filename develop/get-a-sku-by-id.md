---
title: ID で SKU を取得する
description: 指定された SKU ID を使用して、指定された製品の SKU を取得します。
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 01/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ed09684463c1e67cdfc96c6d674be50dadae798f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486132"
---
# <a name="get-a-sku-by-id"></a>ID で SKU を取得する


**適用対象**

- パートナー センター

指定された SKU ID を使用して、指定された製品の SKU を取得します。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 製品 ID。 
- SKU ID。 


## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


特定の SKU の詳細を取得するには、まず「 [ID で製品を取得](get-a-product-by-id.md)する」の手順に従って、特定の製品の操作のインターフェイスを取得します。 生成されたインターフェイスから**sku**プロパティを選択して、sku で使用可能な操作を含むインターフェイスを取得します。 SKU ID を**ById ()** メソッドに渡し、 **Get ()** または**GetAsync ()** を呼び出して sku の詳細を取得します。

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId; 
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求


**要求の構文**

| メソッド  | 要求 URI                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}? country = {country-CODE} HTTP/1.1   |

 

**URI パラメーター**

指定された SKU ID を使用して、指定された製品の SKU を取得するには、次のパスとクエリパラメーターを使用します。

| 名前                   | 種類     | 必須 | 説明                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| 製品 id             | string   | 〇      | 製品を識別する文字列。                           |
| sku-id                 | string   | 〇      | SKU を識別する文字列。                               |
| 国-コード           | string   | 〇      | 国/地域 ID。                                            |

 

**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3V/skus/00G1?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答


成功した場合、応答本文には[SKU](product-resources.md#sku)リソースが含まれます。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

このメソッドは、次のエラーコードを返します。

| HTTP 状態コード     | エラー コード   | 説明                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | 製品が見つかりませんでした。                                                                                    |
| 404                  | 400018       | Sku が見つかりませんでした。                                                                                        |


**応答の例**

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23,956eae17-7650-4470-94d2-4f61b9b02a23
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f,e0ae69a5-6322-4d7e-809d-59e02b51d71f
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNWXHNrdXNcMDBHMQ==?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 17:43:25 GMT
Content-Length: 1108

{
    "id": "00G1",
    "productId": "DZH318Z0BQ3V",
    "title": "Reserved VM Instance, Standard_D32s_v3, US West 2, 3 Years",
    "description": "Reserved Virtual Machines Instance, Standard_D32s_v3, US West 2, 3 Years",
    "minimumQuantity": 1,
    "maximumQuantity": 999999999,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "AzureSubscriptionRegistration",
        "InventoryCheck"
    ],
    "inventoryVariables": [
        "CustomerId",
        "AzureSubscriptionId"
    ],
    "provisioningVariables": [
        "Scope",
        "SubscriptionId"
    ],
    "dynamicAttributes": {
        "armSkuName": "Standard_D32s_v3",
        "cores": "32",
        "ram": "128",
        "skuDisplayName": "D32s v3",
        "category": "General purpose",
        "armRegionName": "westus2",
        "duration": "3Years",
        "region": "US West 2",
        "diskType": "Ssd"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1/availabilities?country=us",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1?country=us",
            "method": "GET",
            "headers": []
        }
    }
}
```

