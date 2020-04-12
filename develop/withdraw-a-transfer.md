---
title: 転送を取り消す
description: 顧客に対して作成されたサブスクリプションの転送を取り消す方法。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d5b8d990747bdff0f1f83958138a5373a1310e9c
ms.sourcegitcommit: 4b1c10f91962861244c9349d5b9a9ba354b35b24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2020
ms.locfileid: "81220738"
---
# <a name="withdraw-a-transfer"></a>転送を取り消す

適用対象

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター


## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客識別子。 顧客の ID を持っていない場合は、[顧客] リストから顧客を選択し、[アカウント] を選択して、Microsoft ID を保存することで、パートナーセンターで ID を検索できます。
- 既存の転送の転送識別子。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド    | 要求 URI                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| **デリート**| [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1      |

### <a name="uri-parameter"></a>URI パラメーター

顧客を識別するには、次のパスパラメーターを使用します。

| Name            | 種類     | 必須 | 説明                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **顧客 id** | string   | はい      | 顧客を識別する GUID 形式の顧客 id。             |
| **転送 id** | string   | はい      | 転送を識別する GUID 形式の転送 id。             |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。


### <a name="request-example"></a>要求の例

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドはコンテンツを返しません (204)。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
