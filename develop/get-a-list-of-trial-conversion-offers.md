---
title: 試用版変換プランの一覧を取得する
description: 評価版変換プランの一覧を取得する方法。
ms.assetid: 7B97505F-10B9-4ACD-9307-111FC1E7D042
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 73e8a8752c0e4a754992ce8ccbbeffc9f9df7bca
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74490072"
---
# <a name="get-a-list-of-trial-conversion-offers"></a>試用版変換プランの一覧を取得する


**適用対象**

- パートナー センター

評価版変換プランの一覧を取得する方法。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。
- 顧客識別子。
- アクティブな試用版サブスクリプションのサブスクリプション ID。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


使用可能な試用変換の一覧を取得するには、まず、顧客 ID と共に[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを使用して顧客を識別します。 次に、試用版サブスクリプション ID を使用して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)メソッドを呼び出すことにより、サブスクリプション操作へのインターフェイスを取得します。 次に、"[**変換**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions)" プロパティを使用して、変換で使用可能な操作のインターフェイスを取得し、 [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get)または[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync)メソッドを呼び出して、使用可能な[**変換**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion)の提供のコレクションを取得します。

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId; 

// Get the available conversions.
var conversions = 
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求


**要求の構文**

| メソッド  | 要求 URI                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1 |

 

**URI パラメーター**

次のパスパラメーターを使用して、顧客と試用版のサブスクリプションを識別します。

| 名前            | 種類   | 必須 | 説明                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| 顧客 id     | string | 〇      | 顧客を識別する GUID 形式の文字列。           |
| サブスクリプション id | string | 〇      | 評価版サブスクリプションを識別する GUID 形式の文字列。 |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> REST 応答


成功した場合、応答本文には[変換](conversions-resources.md#conversionresult)リソースのコレクションが含まれます。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 305
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CV: feJByqU1X0ObaTQr.0
MS-ServerId: 030011719
Date: Thu, 15 Jun 2017 23:10:01 GMT

{
    "totalCount": 1,
    "items": [{
            "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
            "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
            "orderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
            "quantity": 25,
            "billingCycle": "monthly",
            "attributes": {
                "objectType": "Conversion"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 




