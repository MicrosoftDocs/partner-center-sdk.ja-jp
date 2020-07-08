---
title: セルフ サービス ポリシーを更新する
description: セルフサービスポリシーを更新する方法。
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23816461daab4339d35e19a1004a69fa8f713acf
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095584"
---
# <a name="update-a-selfservepolicy"></a>SelfServePolicy を更新する

**適用対象:**

- パートナー センター

このトピックでは、セルフサービスポリシーを更新する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証がサポートされます。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法   | 要求 URI                                                       |
|----------|-------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1 |

### <a name="request-headers"></a>要求ヘッダー

- 要求 ID と相関 ID が必要です。
- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

次の表では、要求本文に必要なプロパティについて説明します。

| 名前                              | Type   | Description                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)| object | セルフサービスポリシー情報。 |

#### <a name="selfservepolicy"></a>SelfServePolicy

次の表では、新しいセルフサービスポリシーを作成するために必要な[SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)リソースの最小限の必須フィールドについて説明します。

| プロパティ              | Type             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | string           | セルフサービスポリシーが正常に作成されたときに提供される、セルフサービスポリシー識別子。     |
| SelfServeEntity       | SelfServeEntity  | アクセスが許可されているセルフサービスエンティティ。                                                     |
| Grantor               | Grantor          | アクセスを許可している権限の許可。                                                                    |
| アクセス許可           | アクセス許可の配列| [アクセス許可](self-serve-policy-resources.md#permission)リソースの配列。                                                      |
| ETag                  | string           | Etag。                                                                                               |


### <a name="request-example"></a>要求の例

```http
PUT https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive

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

## <a name="rest-response"></a>REST 応答

成功した場合、この API は更新されたセルフサービスポリシーの[SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)リソースを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

このメソッドは、次のエラーコードを返します。

| HTTP 状態コード     | エラー コード   | 説明                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | セルフサービスポリシーが見つかりませんでした                                            |
| 404                  | 600040       | セルフサービスポリシー識別子が正しくありません                                  |


### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 Ok
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

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
        "etag": "\"1ec98034-a249-46f4-b9dd-9cd464fb5e47\"",
        "objectType": "SelfServePolicy"
    }
}
```
