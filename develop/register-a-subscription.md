---
title: サブスクリプションを登録する
description: Azure 予約の注文が有効になるように、既存のサブスクリプションを登録します。
ms.assetid: 9B853BF2-855C-4EB3-BBE5-7ECC1336AE08
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 3c5fd478782fa9437fabddf7fd4391069d12739f
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415494"
---
# <a name="register-a-subscription"></a>サブスクリプションを登録する


**適用対象**

- Partner Center

Azure 予約の注文が有効になるように、既存の[サブスクリプション](subscription-resources.md)を登録します。  

Azure 予約を購入するには、少なくとも1つの既存の CSP Azure サブスクリプションが必要です。 この方法では、既存の CSP Azure サブスクリプションを登録し、Azure 予約を購入できるようにすることができます。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客 ID (顧客-テナント id)。 顧客の ID を持っていない場合は、[顧客] リストから顧客を選択し、[アカウント] を選択して、Microsoft ID を保存することで、パートナーセンターで ID を検索できます。
- サブスクリプション ID。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


顧客のサブスクリプションを登録するには、顧客 ID を指定して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出し、顧客を識別することによって、サブスクリプション操作へのインターフェイスを取得します。 次に、サブスクリプション ID を指定して[**ById ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)メソッドを呼び出し、登録するサブスクリプションを識別します。 

最後に、 **register ()** メソッドを呼び出してサブスクリプションを登録し、サブスクリプションの登録状態を取得するために使用できる URI を取得します。 詳細については、「[サブスクリプション登録状態の取得](get-subscription-registration-status.md)」を参照してください。

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求


**要求の構文**

| メソッド    | 要求 URI                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **POST**  | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1 |

 

**URI パラメーター**

次のパスパラメーターを使用して、顧客とサブスクリプションを識別します。 

| Name                    | 種類       | 必須 | 説明                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| 顧客 id             | string     | はい      | 顧客を識別する GUID 形式の文字列。         |
| サブスクリプション id         | string     | はい      | サブスクリプションを識別する GUID 形式の文字列。     |

 

**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

[なし]。

**要求の例**

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

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST 応答


成功した場合、応答には、サブスクリプションの登録状態を取得するために使用できる URI を含む**Location**ヘッダーが含まれます。 他の関連する REST Api で使用するために、この URI を保存します。 状態を取得する方法の例については、「[サブスクリプション登録状態の取得](get-subscription-registration-status.md)」を参照してください。 

**応答成功およびエラーコード**

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

**応答の例**

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```

 

 




