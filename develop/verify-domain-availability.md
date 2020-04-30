---
title: ドメインが使用できるかどうかを確認する
description: ドメインが使用可能かどうかを確認する方法。
ms.assetid: 9ECF8241-3672-441D-B34D-83F7C23138B3
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7518253d937567e78c5afd59b9b0a1375d047c89
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157844"
---
# <a name="verify-domain-availability"></a>ドメインが使用できるかどうかを確認する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

ドメインが使用可能かどうかを確認する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- ドメイン (など`contoso.onmicrosoft.com`)。

## <a name="c"></a>C\#

ドメインが使用可能かどうかを確認するには、まず[**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.domains)を呼び出して、ドメイン操作へのインターフェイスを取得します。 次に、ドメインで[**bydomain**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain)メソッドを呼び出して確認します。 このメソッドは、特定のドメインで使用可能な操作に対するインターフェイスを取得します。 最後に、 [**exists**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists)メソッドを呼び出して、ドメインが既に存在するかどうかを確認します。

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: CheckDomainAvailability.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法   | 要求 URI                                                              |
|----------|--------------------------------------------------------------------------|
| **矢印** | [*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

ドメインの可用性を確認するには、次のクエリパラメーターを使用します。

| 名前       | Type       | 必須 | 説明                                   |
|------------|------------|----------|-----------------------------------------------|
| **domain** | **string** | Y        | チェック対象のドメインを識別する文字列。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし

### <a name="request-example"></a>要求の例

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

## <a name="rest-response"></a>REST 応答

ドメインが存在する場合は使用できず、応答状態コード 200 OK が返されます。 ドメインが見つからない場合は、そのドメインが使用可能であり、応答状態コード "404 が見つかりません" が返されます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example-for-when-the-domain-is-already-in-use"></a>ドメインが既に使用されている場合の応答の例

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a>ドメインが使用可能な場合の応答の例

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
