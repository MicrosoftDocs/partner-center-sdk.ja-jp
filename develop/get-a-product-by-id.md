---
title: ID で製品を取得する
description: 製品 ID を使用して、指定された製品リソースを取得します。
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 8aca626597e9ec903ebecca7d55577ba636c518e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097162"
---
# <a name="get-a-product-by-id"></a>ID で製品を取得する

**適用対象**

- パートナー センター

製品 ID を使用して、指定された製品リソースを取得します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 製品 ID。

## <a name="c"></a>C\#

ID で特定の製品を検索するには、 **iaggregatepartner.customers**コレクションを使用し、 **bycountry ()** メソッドを使用して国を選択してから、 **ById ()** メソッドを呼び出します。 最後に、 **Get ()** または**GetAsync ()** メソッドを呼び出して、製品を返します。

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

ID で特定の製品を検索するには、 **iaggregatepartner.customers**関数を使用し、 **bycountry ()** 関数を使用して国を選択してから、 **byId ()** 関数を呼び出します。 最後に、 **get ()** 関数を呼び出して製品を返します。

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

ID で特定の製品を検索するには、 [**Get partnerproduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md)コマンドを実行し、 **ProductId**パラメーターを指定します。 **CountryCode**パラメーターが指定されていない場合は、販売店に関連付けられている国が使用されます。

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}? country = {COUNTRY} HTTP/1.1  |

### <a name="uri-parameter"></a>URI パラメーター

次のパスパラメーターを使用して、指定された製品を取得します。

| 名前                   | Type     | 必須 | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| 製品 id             | string   | はい      | 製品を識別する文字列。                           |
| country                | string   | はい      | 国/地域 ID。                                            |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[製品](product-resources.md#product)リソースが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

このメソッドは、次のエラーコードを返します。

| HTTP 状態コード     | エラー コード   | 説明                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 400013       | 製品が見つかりませんでした。                                                     |

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "DZH318Z0BQ3Q",
    "title": "Virtual Machines DSv2 Series",
    "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "VirtualMachines",
            "displayName": "VirtualMachines"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3Q?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
