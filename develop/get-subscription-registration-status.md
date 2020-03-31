---
title: サブスクリプション登録状態の取得
description: Azure Reserved VM Instances で使用するように登録されているサブスクリプションの状態を取得します。
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0671ab9bfc9bf254a9bc5472c4ed0f65153af1af
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416622"
---
# <a name="get-subscription-registration-status"></a>サブスクリプション登録状態の取得 

**適用対象**

- Partner Center

Azure Reserved VM Instances 購入が有効になっている顧客サブスクリプションのサブスクリプション登録状態を取得する方法。  

パートナーセンター API を使用して Azure 予約 VM インスタンスを購入するには、少なくとも1つの既存の CSP Azure サブスクリプションが必要です。 [サブスクリプションの登録](register-a-subscription.md)方法を使用すると、既存の CSP Azure サブスクリプションを登録し、Azure Reserved VM Instances を購入できるようになります。 このメソッドを使用すると、その登録の状態を取得できます。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客 ID (顧客-テナント id)。 顧客の ID を持っていない場合は、[顧客] リストから顧客を選択し、[アカウント] を選択して、Microsoft ID を保存することで、パートナーセンターで ID を検索できます。
- サブスクリプション ID。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


サブスクリプションの登録状態を取得するには、まず、顧客 ID を指定して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを使用して顧客を識別します。 次に、サブスクリプションを識別するためにサブスクリプション ID を指定して[**ById ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)メソッドを呼び出すことにより、サブスクリプション操作へのインターフェイスを取得します。 次に、RegistrationStatus プロパティを使用して、現在のサブスクリプションの登録状態操作へのインターフェイスを取得し、 **Get**または**GetAsync**メソッドを呼び出して**subscriptionregistrationstatus**オブジェクトを取得します。

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求

**要求の構文**

| メソッド    | 要求 URI                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **GET**  | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1 |

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
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
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

成功した場合、応答本文には[Subscriptionregistrationstatus](subscription-resources.md#subscriptionregistrationstatus)リソースが含まれます。  

**応答成功およびエラーコード**

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```