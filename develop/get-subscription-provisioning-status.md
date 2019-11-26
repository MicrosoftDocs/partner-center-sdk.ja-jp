---
title: サブスクリプションのプロビジョニング状態の取得
description: 顧客サブスクリプションのサブスクリプションのプロビジョニング状態を取得する方法。
ms.assetid: CC3A13FE-D6D3-4A65-981F-0235A4A8382E
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0e08342b3d712a38dee857b06095e41a6fe9df24
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487152"
---
# <a name="get-subscription-provisioning-status"></a>サブスクリプションのプロビジョニング状態の取得

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

顧客サブスクリプションのサブスクリプションのプロビジョニング状態を取得する方法。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。
- 顧客識別子。
- サブスクリプション識別子。
- この操作を実行するには、サブスクリプションに対する委任された管理者権限が必要です。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


サブスクリプションのプロビジョニング状態を取得するには、まず、顧客 ID と共に[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを使用して顧客を識別します。 次に、サブスクリプション ID を使用して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)メソッドを呼び出すことにより、サブスクリプション操作へのインターフェイスを取得します。 次に、provisioning [**status**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus)プロパティを使用して、現在のサブスクリプションのプロビジョニング状態操作へのインターフェイスを取得してから、 [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get)または[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync)メソッドを呼び出して[**subscriptionprovisioning status**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus)オブジェクトを取得します。

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId; 

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求


**要求の構文**

| メソッド  | 要求 URI                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1 |

 

**URI パラメーター**

次のパスパラメーターを使用して、顧客とサブスクリプションを識別します。

| 名前            | 種類   | 必須 | 説明                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| 顧客 id     | string | 〇      | 顧客を識別する GUID 形式の文字列。     |
| サブスクリプション id | string | 〇      | サブスクリプションを識別する GUID 形式の文字列。 |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答


成功した場合、応答本文には[Subscriptionプロビジョニング状態](subscription-resources.md#subscriptionprovisioningstatus)リソースが含まれます。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344
Date: Thu, 20 Apr 2017 19:23:39 GMT

{
    "skuId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
    "status": "success",
    "quantity": 5,
    "endDate": "2018-05-10T00:00:00Z",
    "attributes": {
        "objectType": "SubscriptionProvisioningStatus"
    }
}
```

## <a name="span-idremarksspan-idremarksspan-idremarksremarks"></a><span id="Remarks"/><span id="remarks"/><span id="REMARKS"/>解説

- 接続クライアントの割り当ての変更時に、 [subscriptionの](subscription-resources.md#subscriptionprovisioningstatus)状態フィールドが "pending" に設定されます。
- [状態] フィールドは、15分ごとに更新されます。