---
title: パートナーの MPN ID を検証する
description: パートナーの Microsoft Partner Network 識別子 (MPN ID) を確認する方法。次に示す手法では、パートナーセンターからパートナーの MPN プロファイルを要求することによって、パートナーの Microsoft Partner Network 識別子を確認します。
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5c35cfb024a8894d7f40208f8f93f6f41ee94121
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095214"
---
# <a name="verify-a-partner-mpn-id"></a>パートナーの MPN ID を検証する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーの Microsoft Partner Network 識別子 (MPN ID) を確認する方法。

次に示す手法では、パートナーセンターからパートナーの MPN プロファイルを要求することによって、パートナーの Microsoft Partner Network 識別子を確認します。 この識別子は、要求が成功した場合に有効と見なされます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 確認するパートナー MPN ID。 この値を省略した場合、要求はサインインしているパートナーの MPN プロファイルを取得します。

## <a name="c"></a>C\#

パートナーの MPN ID を確認するには、まず、 [**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.profiles)プロパティからパートナープロファイルコレクション操作へのインターフェイスを取得します。 次に、 [**Mpnprofile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile)プロパティから MPN profile 操作へのインターフェイスを取得します。 最後に、MPN ID を使用して[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get)メソッドまたは[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync)メソッドを呼び出し、MPN プロファイルを取得します。 Get または GetAsync 呼び出しから MPN ID を省略した場合、要求はサインインしているパートナーの MPN プロファイルを取得しようとします。

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: VerifyPartnerMpnId.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/V1/profiles/mpn? mpnid = {MPN} HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを指定して、パートナーを識別します。 このクエリパラメーターを省略すると、要求によって、サインインしているパートナーの MPN プロファイルが返されます。

| 名前   | Type | 必須 | 説明                                                 |
|--------|------|----------|-------------------------------------------------------------|
| mpn-id | INT  | いいえ       | パートナーを識別する Microsoft Partner Network ID。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn?mpnId=9999999 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には、パートナーの[Mpnprofile](profile-resources.md#mpnprofile)リソースが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example-success"></a>応答の例 (成功)

```http
HTTP/1.1 200 OK
Content-Length: 159
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: e39e0ddf-3fd0-4b7e-bb4e-8aebe242d3ee
MS-CV: s2GvkNgZsUSadxQX.0
MS-ServerId: 030011719
Date: Thu, 13 Apr 2017 18:13:40 GMT

{
    "mpnId": "4391507",
    "profileType": "MpnProfile",
    "links": {
        "self": {
            "uri": "/profiles/mpn",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "MpnProfile"
    }
}
```

### <a name="response-example-failure"></a>応答の例 (失敗)

```http
HTTP/1.1 404 Not Found
Content-Length: 124
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CV: sLRFZMWm+EKuL47u.0
MS-ServerId: 102030524
Date: Thu, 13 Apr 2017 18:26:51 GMT

{
    "code": 3000,
    "description": "Partner Organization with partner_id 9999999 could not be found",
    "data": [],
    "source": "PartnerFD"
}
```
