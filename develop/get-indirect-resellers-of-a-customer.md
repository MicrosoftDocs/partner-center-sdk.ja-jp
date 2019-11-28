---
title: 顧客の間接リセラーを取得する
description: 指定された顧客との関係を持つ間接リセラーの一覧を取得する方法。
ms.assetid: C3C4BE9A-97E8-41AD-AB28-6F9CB7DCE475
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 338240998f61bb35185e75459ba8291e4683fc6d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489462"
---
# <a name="get-indirect-resellers-of-a-customer"></a>顧客の間接リセラーを取得する

**適用対象**

- パートナー センター

指定された顧客との関係を持つ間接リセラーの一覧を取得する方法。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。
- 顧客識別子。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


指定された顧客がリレーションシップを持つ間接リセラーの一覧を取得するには、まず、顧客を識別するための顧客 ID を指定して、特定の顧客の顧客コレクション操作へのインターフェイスを取得します[ **。** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) 次に、リレーションシップを呼び出して、間接リセラーの一覧を取得するために[ **\_非同期**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync)メソッドを取得または取得し[**ます。** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get)

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)**プロジェクト**: パートナーセンター SDK サンプル**クラス**: GetIndirectResellersOfCustomer.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求の構文**

| メソッド  | 要求 URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1 |

 

**URI パラメーター**

顧客を識別するには、次のパスパラメーターを使用します。

| 名前        | 種類   | 必須 | 説明                                           |
|-------------|--------|----------|-------------------------------------------------------|
| 顧客 id | string | 〇      | 顧客を識別する GUID 形式の文字列。 |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答

成功した場合、応答本文には、再販業者を識別するための[Partnerrelationship](relationships-resources.md)リソースのコレクションが含まれます。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 264
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CV: plJP3ufU0UqXMeuh.0
MS-ServerId: 020021921
Date: Fri, 07 Apr 2017 23:42:11 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "mpnId": "4847383",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```