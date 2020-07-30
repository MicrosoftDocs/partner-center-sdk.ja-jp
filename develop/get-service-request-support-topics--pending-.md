---
title: サービス要求のサポート トピックを取得する
description: サービス要求に関する有効なトピックを表す項目のコレクションを取得します。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e16348d9342c0c3d60debd0bc6ea7d2146edca27
ms.sourcegitcommit: 68a5497a7350e135358aeb7f2a54c75707f922c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87261921"
---
# <a name="get-service-request-support-topics"></a>サービス要求のサポート トピックを取得する

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

サービス要求に関する有効なトピックを表す項目のコレクションを取得します。

   > [!IMPORTANT]
   > Get service request support トピック API は、2020年8月31日までにサポートされなくなります。 この API は、必要なデータをプログラムによって取得し、使用停止になっているサービス要求 API を作成するために、パートナーによって使用されました。 パートナーがパートナーサポートチケットを作成するには、パートナーセンターのユーザーインターフェイスを使用する必要があります。 ユーザーエクスペリエンスでは、問題が発生している領域について推奨される手順やドキュメントなどのサポートケースを作成する際に、パートナーの追加情報を提供します。 また、パートナーセンターチームは、サポートエンジニアが問題を迅速かつ正確に解決するために必要な問題領域に固有の情報を要求するサービス要求フォームをカスタマイズすることで、ユーザーエクスペリエンスを向上させました。


## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

## <a name="c"></a>C\#

サービス要求トピックのコレクションを取得するには、 [**Ipartneroperations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner)コレクションを使用して、結果として得られるオブジェクトの[**ServiceRequests**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.servicerequests)プロパティを取得します。次に、 [**supporttopics**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.isupporttopicscollection)プロパティと[**get ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.isupporttopicscollection.get)メソッドまたは[**GetAsync ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.isupporttopicscollection.getasync)メソッドを使用します。

``` csharp
// IPartner partnerOperations;

ResourceCollection<SupportTopic> supportTopicsCollection = partnerOperations.ServiceRequests.SupportTopics.Get();
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                           |
|---------|---------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/supporttopics HTTP/1.1 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

ありません。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/servicerequests/supporttopics HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4c1e8b6c-d136-4931-9df9-d85ec08ccffe
MS-CorrelationId: f447b215-f9bc-48da-a05a-3b5322d86a9c
X-Locale: en-US
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドはサポート要求に関する有効なトピックのコレクションを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 4982
Content-Type: application/json
MS-CorrelationId: f447b215-f9bc-48da-a05a-3b5322d86a9c
MS-RequestId: 4c1e8b6c-d136-4931-9df9-d85ec08ccffe
Date: Fri, 29 Jan 2016 22:31:36 GMT

{
    "totalCount":14,
    "items":[{
        "name":"Partner Center Issues",
        "description":"Office 365 questions from the CSP (Cloud Solution Provider) partners using Partner Center",
        "id":32444667,
        "attributes":{
            "objectType":"SupportTopic"
        }
    },
    {
        "name":"Cannot manage my profile",
        "description":"Issues that are related to errors or problems with managing a profile",
        "id":32444671,
        "attributes":{
            "objectType":"SupportTopic"
        }
    }],
    "attributes":{
        "objectType":"Collection"
    }
}
```
