---
title: サブスクリプションの Azure の権利の一覧を取得する
description: AzureEntitlement リソースを使用して、サブスクリプションに属している Azure の権利リソースのコレクションを取得できます。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d2aaaed8fd4455cc2e7b57281ea1e104fdbe030c
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412295"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a>サブスクリプションの Azure の権利の一覧を取得する

適用対象

- Partner Center

[Azure の権利リソース](subscription-resources.md#azureentitlement)(**azureentitlement**) を使用して、サブスクリプションに属するリソースのコレクションを取得できます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客 ID (**customer-tenant-id**)。 顧客の id を持っていない場合は、顧客 一覧から顧客を選択し、**アカウント** を選択して、 **Microsoft ID**を保存することで、パートナーセンターで検索できます。
- サブスクリプション識別子。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド  | 要求 URI                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

次の表に、サブスクリプションのすべての Azure 権限を取得するために必要なクエリパラメーターを示します。

| Name                   | 種類     | 必須 | 説明                           |
|------------------------|----------|----------|---------------------------------------|
| **顧客-テナント id** | **guid** | Y        | 顧客に対応する GUID。 |
| **サブスクリプション id**       | **guid** | Y        | サブスクリプションに対応する GUID。    |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし]。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で[**Azureentitlement**](subscription-resources.md#azureentitlement)リソースのコレクションを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 04 Oct 2019 05:50:45 GMT

{
"totalCount":1,
"items":[
  {
    "id":"899ae6f1-8a74-4d5e-b6c6-e6b5019bbff8",
    "friendlyName":"Microsoft Azure",
    "status":"active",
    "subscriptionId":"3f15978e-005c-b763-bb78-2a8fab289c58"
   }],
    "attributes":{"objectType":"Collection"}
  }
