---
title: 間接リセラーの一覧を取得する
description: サインインしているパートナーの間接リセラーの一覧を取得する方法。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e8615438d8ecd011fd1f00a5672b78d53f7bd77d
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926415"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>間接リセラーの一覧を取得する

**適用対象**

- パートナー センター

サインインしているパートナーの間接リセラーの一覧を取得する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

## <a name="c"></a>C\#

サインインパートナーに関係がある間接リセラーの一覧を取得するには、まず、[**partneroperations**] プロパティからリレーションシップコレクション操作へのインターフェイスを取得します。 次に、[**/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get)** または [**get \_ Async**/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) メソッドを呼び出し、[**partnerrelationshiptype**/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) 列挙型のメンバーを渡してリレーションシップの種類を識別します。 間接リセラーを取得するには、IsIndirectCloudSolutionProviderOf を使用する必要があります。

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**サンプル**: [コンソールテストアプリ](console-test-app.md)**プロジェクト**: パートナーセンター SDK サンプル **クラス**: GetIndirectResellers.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/relationships? リレーションシップの \_ 種類 = IsIndirectCloudSolutionProviderOf HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

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
<td>はい</td>
<td>値は、 <a href="https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype"><strong>Partnerrelationshiptype</strong></a>で見つかったいずれかのメンバー名の文字列表現です。
<p>パートナーがプロバイダーとしてサインインしている場合に、関係を確立した間接リセラーの一覧を取得するには、IsIndirectCloudSolutionProviderOf を使用します。</p>
<p>パートナーが再販業者としてサインインしている場合に、関係を確立した間接プロバイダーの一覧を取得するには、IsIndirectResellerOf を使用します。</p></td>
</tr>
</tbody>
</table>

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には、再販業者を識別するための [Partnerrelationship](relationships-resources.md) リソースのコレクションが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「 [パートナーセンターのエラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

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
