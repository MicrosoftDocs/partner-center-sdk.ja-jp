---
title: パートナー MPN ID を確認する
description: パートナーの Microsoft Partner Network 識別子 (MPN ID) を確認する方法。次に示す手法では、パートナーセンターからパートナーの MPN プロファイルを要求することによって、パートナーの Microsoft Partner Network 識別子を確認します。
ms.assetid: 95CBA254-0980-4519-B95D-1F906C321863
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cc18ee559bd3ceafd7239ccb46e7d616d8fc5f13
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415699"
---
# <a name="verify-a-partner-mpn-id"></a>パートナー MPN ID を確認する

**適用対象**

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーの Microsoft Partner Network 識別子 (MPN ID) を確認する方法。

次に示す手法では、パートナーセンターからパートナーの MPN プロファイルを要求することによって、パートナーの Microsoft Partner Network 識別子を確認します。 この識別子は、要求が成功した場合に有効と見なされます。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。
- 確認するパートナー MPN ID。 この値を省略した場合、要求はサインインしているパートナーの MPN プロファイルを取得します。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#

パートナーの MPN ID を確認するには、まず、 [**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.profiles)プロパティからパートナープロファイルコレクション操作へのインターフェイスを取得します。 次に、 [**Mpnprofile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile)プロパティから MPN profile 操作へのインターフェイスを取得します。 最後に、MPN ID を使用して[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get)メソッドまたは[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync)メソッドを呼び出し、MPN プロファイルを取得します。 Get または GetAsync 呼び出しから MPN ID を省略した場合、要求はサインインしているパートナーの MPN プロファイルを取得しようとします。

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: VerifyPartnerMpnId.cs

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求


**要求の構文**

| メソッド  | 要求 URI                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/V1/profiles/mpn? mpnid = {MPN} HTTP/1.1 |

**URI パラメーター**

次のクエリパラメーターを指定して、パートナーを識別します。 このクエリパラメーターを省略すると、要求によって、サインインしているパートナーの MPN プロファイルが返されます。

| Name   | 種類 | 必須 | 説明                                                 |
|--------|------|----------|-------------------------------------------------------------|
| mpn-id | int  | いいえ       | パートナーを識別する Microsoft Partner Network ID。 |

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

[なし]。

**要求の例**

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

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> REST 応答

成功した場合、応答本文には、パートナーの[Mpnprofile](profile-resources.md#mpnprofile)リソースが含まれます。

**応答成功およびエラーコード**

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

**応答の例 (成功)**

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

**応答の例 (失敗)**

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