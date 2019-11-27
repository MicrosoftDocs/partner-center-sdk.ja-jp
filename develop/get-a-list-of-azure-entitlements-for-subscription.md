---
title: サブスクリプションの Azure の権利の一覧を取得する
description: AzureEntitlement リソースを使用して、サブスクリプションに属している Azure の権利リソースのコレクションを取得できます。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 788ad84ca128995067886f67fa70c17239cfd95a
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487502"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a>サブスクリプションの Azure の権利の一覧を取得する

適用対象:

- パートナー センター

[Azure の権利リソース](subscription-resources.md#azureentitlement)(**azureentitlement**) を使用して、サブスクリプションに属するリソースのコレクションを取得できます。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客識別子 (**顧客-テナント id**)。 顧客の id を持っていない場合は、顧客 一覧から顧客を選択し、**アカウント** を選択して、 **Microsoft ID**を保存することで、パートナーセンターで検索できます。
- サブスクリプション識別子。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド  | 要求 URI                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

次の表に、サブスクリプションのすべての Azure 権限を取得するために必要なクエリパラメーターを示します。

| 名前                   | 種類     | 必須 | 説明                           |
|------------------------|----------|----------|---------------------------------------|
| **顧客-テナント id** | **guid** | Y        | 顧客に対応する GUID。 |
| **サブスクリプション id**       | **guid** | Y        | サブスクリプションに対応する GUID。    |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>要求本文

なし。

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

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

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
