---
title: 市場別のプラン カテゴリの一覧を取得する
description: 特定の国/地域およびロケールのすべてのオファーカテゴリを含むコレクションを取得する方法。
ms.assetid: 69174433-74C6-4294-ACAA-C2CE3D69CFEE
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0cb3d64444558b301fb1f5991f8d5e78c58c53b2
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156874"
---
# <a name="get-a-list-of-offer-categories-by-market"></a>市場別のプラン カテゴリの一覧を取得する

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

この記事では、特定の国/地域とロケールのすべてのオファーカテゴリを含むコレクションを取得する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

## <a name="c"></a>C\#

特定の国/地域とロケールでプランカテゴリの一覧を取得するには、次のようにします。

1. [**Iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.iaggregatepartner)コレクションを使用して、特定のコンテキストで[**With ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with)メソッドを呼び出します。

2. 結果として得られるオブジェクトの[**OfferCategories**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories)プロパティを調べます。

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

例については、以下を参照してください。

- サンプル:[コンソールテストアプリ](console-test-app.md)
- プロジェクト: **Partnersdk. FeatureSample**
- クラス: **Partnersdk. FeatureSample**

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories? country = {country-ID} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

次の表に、プランのカテゴリを取得するために必要なクエリパラメーターを示します。

| 名前           | Type       | 必須 | 説明            |
|----------------|------------|----------|------------------------|
| **country-id** | **string** | Y        | 国/地域 ID。 |

### <a name="request-headers"></a>要求ヘッダー

文字列として書式設定された**ロケール id**が必要です。

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で**OfferCategory**リソースのコレクションを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
