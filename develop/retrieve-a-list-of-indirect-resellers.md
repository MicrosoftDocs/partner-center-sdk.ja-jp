---
title: 間接リセラーの一覧を取得する
description: サインインしているパートナーの間接リセラーの一覧を取得する方法。
ms.assetid: 1767BD6C-651A-4C14-930B-35D7EFD46C19
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e796312e76038174329967d106eefb4ac40d629f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486532"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>間接リセラーの一覧を取得する


**適用対象**

- パートナー センター

サインインしているパートナーの間接リセラーの一覧を取得する方法。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


サインインしているパートナーが関係を持つ間接リセラーの一覧を取得するには、まず、 [**partneroperations.** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) relationship プロパティからリレーションシップコレクション操作へのインターフェイスを取得します。 次に、 [**get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get)または[**get\_Async**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync)メソッドを呼び出し、 [**partnerrelationshiptype**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype)列挙体のメンバーを渡してリレーションシップ型を識別します。 間接リセラーを取得するには、IsIndirectCloudSolutionProviderOf を使用する必要があります。

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)**プロジェクト**: パートナーセンター SDK サンプル**クラス**: GetIndirectResellers.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求の構文**

| メソッド  | 要求 URI                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/relationships? リレーションシップ\_Type = IsIndirectCloudSolutionProviderOf HTTP/1.1 |

 

**URI パラメーター**

リレーションシップの種類を識別するには、次のクエリパラメーターを使用します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>relationship_type</td>
<td>string</td>
<td>〇</td>
<td>値は、 <a href="https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype"><strong>Partnerrelationshiptype</strong></a>で見つかったいずれかのメンバー名の文字列表現です。
<p>パートナーがプロバイダーとしてサインインしている場合に、関係を確立した間接リセラーの一覧を取得するには、IsIndirectCloudSolutionProviderOf を使用します。</p>
<p>パートナーが再販業者としてサインインしている場合に、関係を確立した間接プロバイダーの一覧を取得するには、IsIndirectResellerOf を使用します。</p></td>
</tr>
</tbody>
</table>

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
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
Content-Length: 298
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CV: b21Ll1miM0yFMPQQ.0
MS-ServerId: 030020643
Date: Wed, 05 Apr 2017 21:08:44 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847383",
            "location": "US",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }, {
            "id": "b01b1487-b36e-4e6d-9b5e-0b58974c4b28",
            "name": "ReleCloud",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847433",
            "location": "BR",
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

 

 




