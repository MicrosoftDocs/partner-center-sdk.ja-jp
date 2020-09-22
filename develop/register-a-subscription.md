---
title: サブスクリプションを登録する
description: Azure 予約の注文が有効になるように、既存のサブスクリプションを登録します。
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3cabfd9d2bba309d773f15b2de2a4b33e4575241
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926666"
---
# <a name="register-a-subscription"></a>サブスクリプションを登録する

**適用対象**

- パートナー センター

Azure 予約の注文が有効になるように、既存の [サブスクリプション](subscription-resources.md) を登録します。

Azure 予約を購入するには、少なくとも1つの既存の CSP Azure サブスクリプションが必要です。 この方法では、既存の CSP Azure サブスクリプションを登録し、Azure 予約を購入できるようにすることができます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- サブスクリプション ID。

## <a name="c"></a>C\#

顧客のサブスクリプションを登録するには、顧客 ID を指定して [**iaggregatepartner.customers. ById**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) メソッドを呼び出し、顧客を識別するために、サブスクリプション操作へのインターフェイスを取得します。 次に、サブスクリプション ID を指定して [**ById ()**/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) メソッドを呼び出し、登録するサブスクリプションを識別します。

最後に、 **register ()** メソッドを呼び出してサブスクリプションを登録し、サブスクリプションの登録状態を取得するために使用できる URI を取得します。 詳細については、「 [サブスクリプション登録状態の取得](get-subscription-registration-status.md)」を参照してください。

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法    | 要求 URI                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **POST**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1 |

### <a name="uri-parameters"></a>URI パラメーター

次のパスパラメーターを使用して、顧客とサブスクリプションを識別します。

| 名前                    | 種類       | 必須 | 説明                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| customer-id             | string     | はい      | 顧客を識別する GUID 形式の文字列。         |
| subscription-id         | string     | はい      | サブスクリプションを識別する GUID 形式の文字列。     |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答には、サブスクリプションの登録状態を取得するために使用できる URI を含む **Location** ヘッダーが含まれます。 他の関連する REST Api で使用するために、この URI を保存します。 状態を取得する方法の例については、「 [サブスクリプション登録状態の取得](get-subscription-registration-status.md)」を参照してください。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
