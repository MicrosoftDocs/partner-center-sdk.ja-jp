---
title: ID でセルフ サービス ポリシーを取得する
description: ID を使用して、指定されたセルフサービスポリシーを取得します。
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ec01d0d9b7c3858cdacf1dbaad3b2b0bb7b6a1a4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098043"
---
# <a name="get-a-self-serve-policy-by-id"></a>ID でセルフ サービス ポリシーを取得する

**適用対象**

- パートナー センター

ID を使用して、指定されたセルフサービスポリシーを取得します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証がサポートされます。
- セルフサービスポリシー ID。

## <a name="examples"></a>例


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求

**要求の構文**

| Method  | 要求 URI                                                                   |
|---------|-------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1 |

**URI パラメーター**

次のパスパラメーターを使用して、指定された製品を取得します。

| 名前                       | Type         | 必須 | Description                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| **SelfServePolicy-id**     | **string**   | はい      | セルフサービスポリシーを識別する文字列。                 |

**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

[なし] :

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)リソースが含まれます。

**応答の成功とエラーのコード**

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

このメソッドは、次のエラーコードを返します。

| HTTP 状態コード     | エラー コード   | 説明                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | セルフサービスポリシーが見つかりません。                                                     |

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```