---
title: MFA の導入ステータスを取得する
description: パートナー REST API を使用して、パートナーごとに multi-factor authentication の導入状態の一覧を取得します。
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.date: 05/29/2020
ms.openlocfilehash: ac47df306c19194a50b14f000fe4182a437d8c84
ms.sourcegitcommit: 9c3c915b79846917b2075be632d5b9b013f53a27
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84186340"
---
# <a name="get-mfa-adoption-status"></a>MFA の導入ステータスを取得する

適用先:

- パートナー センター API

この記事では、テナント内の各パートナーの multi-factor authentication (MFA) の導入ステータスを取得する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証がサポートされます。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                               |
|---------|---------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus> |

### <a name="request-headers"></a>要求ヘッダー

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/applicationmfaadoptionstatus HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは、応答本文の[アプリケーションリソースによって要約](mfa-resources.md#api-request-summarized-by-application)された API 要求のコレクションを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

``` http
HTTP/1.1 200 OK
Content-Length: 313
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 21 May 2020 22:29:17 GMT
[
    {
        "loginDate": "2020-05-20",
        "mfaCompliantRequestCount": 7,
        "totalRequestCount": 7,
        "applicationId": "14f38d7d-c4fc-448a-b2df-0fc60e75465a",
        "applicationName": ""
    },
    {
        "loginDate": "2020-05-19",
        "mfaCompliantRequestCount": 7,
        "totalRequestCount": 14,
        "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
        "applicationName": ""
    }
]
```
