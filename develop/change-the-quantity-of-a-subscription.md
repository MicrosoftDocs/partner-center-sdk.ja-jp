---
title: サブスクリプションの数量を変更する
description: サブスクリプションを更新して、顧客のライセンスの数を増減させます。
ms.assetid: 10535C45-63BF-4E75-A6E5-E03ADC1DF8DC
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3d4d94d244ca6d2f4c10054f9486e8fd04c514b1
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489002"
---
# <a name="change-the-quantity-of-a-subscription"></a>サブスクリプションの数量を変更する

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

[サブスクリプション](subscription-resources.md)を更新してライセンスの数を増減します。

パートナーセンターのダッシュボードでは、最初に[顧客を選択](get-a-customer-by-name.md)することでこの操作を実行できます。 次に、名前を変更する対象のサブスクリプションを選択します。 完了するには、 **Quantity**フィールドの値を変更し、[送信] を選択し**ます。**

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客 ID (顧客-テナント id)。 顧客の ID を持っていない場合は、[顧客] リストから顧客を選択し、[アカウント] を選択して、Microsoft ID を保存することで、パートナーセンターで ID を検索できます。
- サブスクリプション ID。

## <a name="c"></a>C\#

顧客のサブスクリプションの数量を変更するには、最初に[サブスクリプションを取得](get-a-subscription-by-id.md)してから、サブスクリプションの[**quantity**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity)プロパティを変更します。 変更が完了したら、 **iaggregatepartner.customers**コレクションを使用して、 **ById ()** メソッドを呼び出します。 次に、[**サブスクリプション**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)プロパティを呼び出し、その後に[**ById ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)メソッドを呼び出します。 次に、 **Patch ()** メソッドを呼び出して終了します。

``` csharp
// IAggregatePartner partnerOperations;
// var customerId;
// var subscriptionId;

//retrieving the subscription, for the purpose of the sample
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

//update selected subscription,
selectedSubscription.Quantity++;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: partnersdk. FeatureSample**クラス**: UpdateSubscription.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド    | 要求 URI                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **KB830347** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次の表に、サブスクリプションの数量を変更するために必要なクエリパラメーターを示します。

| 名前                    | 種類     | 必須 | 説明                               |
|-------------------------|----------|----------|-------------------------------------------|
| **顧客-テナント id**  | **guid** | Y        | 顧客に対応する GUID。     |
| **id-サブスクリプション** | **guid** | Y        | サブスクリプションに対応する GUID。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

要求本文には、完全な**サブスクリプション**リソースが必要です。 **Quantity**プロパティが更新されていることを確認します。

### <a name="request-example"></a>要求の例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で**HTTP ステータス 200**状態コードおよび更新された[サブスクリプションリソース](subscription-resources.md)プロパティを返します。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが返されます。 ネットワークトレースツールを使用して、状態コード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

修正プログラムの処理に予想される時間よりも時間がかかる場合、パートナーセンターは、 **HTTP 状態 202**状態コードと、サブスクリプションを取得する場所を指す location ヘッダーを送信します。 サブスクリプションを定期的に照会して、状態と数量の変化を監視することができます。

### <a name="response-examples"></a>応答の例

#### <a name="response-example-1"></a>応答の例1

**HTTP ステータス 200**状態コードで成功した要求:

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

#### <a name="response-example-2"></a>応答の例2

**HTTP ステータス 202**状態コードで成功した要求:

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 01880c1b-1966-40f0-d470-501a66d9948b
MS-CorrelationId: 2c5827c1-d5f9-4835-cc6d-f1918b782c79
Content-Type: application/json
Content-Length: 1432
Connection: Keep-Alive
Location: /customers/<customer-tenant-id>/subscriptions/<subscriptionID>
```