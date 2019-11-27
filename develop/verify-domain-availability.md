---
title: ドメインの可用性を確認する
description: ドメインが使用可能かどうかを確認する方法。
ms.assetid: 9ECF8241-3672-441D-B34D-83F7C23138B3
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 79f68fe92f22a4e5a6793f97b55da16adee19b5a
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486242"
---
# <a name="verify-domain-availability"></a>ドメインの可用性を確認する


**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

ドメインが使用可能かどうかを確認する方法。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- ドメイン (例: "contoso.onmicrosoft.com")。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


ドメインが使用可能かどうかを確認するには、まず[**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.domains)を呼び出して、ドメイン操作へのインターフェイスを取得します。 次に、ドメインで[**bydomain**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain)メソッドを呼び出して確認します。 これにより、特定のドメインで使用可能な操作に対するインターフェイスが取得されます。 最後に、 [**exists**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists)メソッドを呼び出して、ドメインが既に存在するかどうかを確認します。

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";  

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: CheckDomainAvailability.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求の構文**

| メソッド   | 要求 URI                                                              |
|----------|--------------------------------------------------------------------------|
| **矢印** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1 |

 

**URI パラメーター**

ドメインの可用性を確認するには、次のクエリパラメーターを使用します。

| 名前       | 種類       | 必須 | 説明                                   |
|------------|------------|----------|-----------------------------------------------|
| **domain** | **文字列** | Y        | 確認するドメインを識別する文字列。 |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし

**要求の例**

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答


ドメインが存在する場合は使用できず、応答状態コード 200 OK が返されます。 ドメインが見つからない場合は、そのドメインが使用可能であり、応答状態コード "404 が見つかりません" が返されます。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

**ドメインが既に使用されている場合の応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

**ドメインが使用可能な場合の応答の例**

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```

 

 




