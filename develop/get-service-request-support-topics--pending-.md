---
title: サービスリクエストのサポートに関するトピックを取得する
description: サービス要求に関する有効なトピックを表す項目のコレクションを取得します。
ms.assetid: 50A61342-70C4-49F5-BEA2-2754338CF5A1
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 092b0ccb35f907e0b7b3c7cebb33c6e0c2e3c27d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487272"
---
# <a name="get-service-request-support-topics"></a>サービスリクエストのサポートに関するトピックを取得する

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

サービス要求に関する有効なトピックを表す項目のコレクションを取得します。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


サービス要求トピックのコレクションを取得するには、 [**Ipartneroperations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner)コレクションを使用して、結果として得られるオブジェクトの[**ServiceRequests**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.servicerequests)プロパティを取得します。次に、 [**supporttopics**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.isupporttopicscollection)プロパティと[**get ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.isupporttopicscollection.get)メソッドまたは[**GetAsync ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.isupporttopicscollection.getasync)メソッドを使用します。

``` csharp
// IPartner partnerOperations;

ResourceCollection<SupportTopic> supportTopicsCollection = partnerOperations.ServiceRequests.SupportTopics.Get();
```

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求


**要求の構文**

| メソッド  | 要求 URI                                                                           |
|---------|---------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/servicerequests/supporttopics HTTP/1.1 |

 

**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/servicerequests/supporttopics HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4c1e8b6c-d136-4931-9df9-d85ec08ccffe
MS-CorrelationId: f447b215-f9bc-48da-a05a-3b5322d86a9c
X-Locale: en-US
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答


成功した場合、このメソッドはサポート要求に関する有効なトピックのコレクションを返します。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

**応答の例**

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