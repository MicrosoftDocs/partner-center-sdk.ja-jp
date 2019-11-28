---
title: 間接リセラーの顧客の注文を作成する
description: 間接リセラーの顧客の注文を作成する方法。
ms.assetid: 3B89F8CE-96A8-443F-927E-6351E24FDBFF
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 08926408e8cc6cab62a3edf5885724f943f1ccc8
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489542"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>間接リセラーの顧客の注文を作成する

適用対象:

- パートナー センター

間接リセラーの顧客の注文を作成する方法。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。
- 顧客識別子。
- 購入する品目のプラン識別子。
- 間接リセラーのテナント識別子。

## <a name="c"></a>C\#

間接リセラーの顧客の注文を作成するには、次のようにします。

1. サインインしているパートナーとの関係を持つ間接リセラーのコレクションを取得します。
2. 間接リセラー ID に一致するコレクション内の項目に対して、ローカル変数を取得します。 この手順は、注文を作成するときに、リセラーの[**Mpnid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid)プロパティにアクセスするのに役立ちます。
3. 顧客を記録するために、 [**order**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order)オブジェクトをインスタンス化し、 [**ReferenceCustomerID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid)プロパティを顧客 id に設定します。
4. [**Orderlineitem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem)オブジェクトの一覧を作成し、そのリストを注文の[**LineItems**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems)プロパティに割り当てます。 各注文品目には、1つのオファーの購入情報が含まれています。 各品目の[**Partneridonrecord**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord)プロパティに間接リセラーの MPN ID を設定してください。 少なくとも1つの注文品目が必要です。
5. 顧客 ID を指定して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出して顧客を識別し、 [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)プロパティからインターフェイスを取得することによって、注文操作のためのインターフェイスを取得します。
6. 注文を作成するには、 [**create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create)または[**createasync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync)メソッドを呼び出します。

### <a name="c-example"></a>C\# の例

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)**プロジェクト**: パートナーセンター SDK サンプル**クラス**: PlaceOrderForCustomer.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド   | 要求 URI                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **投稿** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

顧客を識別するには、次のパスパラメーターを使用します。

| 名前        | 種類   | 必須 | 説明                                           |
|-------------|--------|----------|-------------------------------------------------------|
| 顧客 id | string | 〇      | 顧客を識別する GUID 形式の文字列。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

#### <a name="order"></a>[オーダー]

次の表では、要求本文の**Order**プロパティについて説明します。

| 名前 | 種類 | 必須 | 説明 |
| ---- | ---- | -------- | ----------- |
| id | string | X | 注文が正常に作成されたときに提供される注文 id。 |
| ReferenceCustomerId | string | 〇 | 顧客識別子。 |
| 周期サイクル | string | X | パートナーがこの注文に対して課金される頻度。 既定値は &quot;毎月の&quot; で、注文が正常に作成されたときに適用されます。 サポートされている値は、 [**BillingCycleType**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype)で見つかったメンバー名です。 注: 年間請求機能は、まだ一般公開されていません。 年次請求のサポートは、間もなくご利用可能になります。 |
| lineItems | オブジェクトの配列 | 〇 | [**Orderlineitem**](#orderlineitem)リソースの配列。 |
| CreationDate | string | X | 注文が作成された日付 (日付/時刻形式)。 注文が正常に作成されたときに適用されます。 |
| 属性 | オブジェクト | X | "ObjectType": "Order" を格納します。 |

#### <a name="orderlineitem"></a>OrderLineItem

次の表では、要求本文の**Orderlineitem**プロパティについて説明します。

| 名前 | 種類 | 必須 | 説明 |
| ---- | ---- | -------- | ----------- |
| LineItemNumber | int | 〇 | コレクション内の各行項目は、0からカウント-1 までカウントされる一意の行番号を取得します。 |
| offerId | string | 〇 | プランの識別子。 |
| subscriptionId | string | X | サブスクリプション識別子。 |
| ParentSubscriptionId | string | X | (省略可能)。 アドオンプランの親サブスクリプションの ID。 PATCH にのみ適用されます。 |
| friendlyName | string | X | (省略可能)。 明確に区別するためにパートナーによって定義されたサブスクリプションのフレンドリ名。 |
| quantity | int | 〇 | ライセンスベースのサブスクリプションのライセンス数。 |
| PartnerIdOnRecord | string | X | 間接プロバイダーが間接リセラーの代わりに注文を行う場合は、このフィールドに**間接リセラー**の MPN id のみを入力します (間接プロバイダーの id は使用しないでください)。 これにより、インセンティブを適切にアカウンティングできます。 **リセラーの MPN ID を指定しないと、注文は失敗しません。ただし、リセラーは記録されません。結果として、インセンティブの計算には売上が含まれない場合があります。** |
| 属性 | オブジェクト | X | "ObjectType": "OrderLineItem" が含まれています。 |

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には、設定された[注文](order-resources.md)リソースが含まれます。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```