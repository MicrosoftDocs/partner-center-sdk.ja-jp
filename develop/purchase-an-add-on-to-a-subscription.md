---
title: サブスクリプションのアドオンを購入する
description: 既存のサブスクリプションにアドオンを購入する方法。
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 69c817cc89b97cea43533c170cef598df99095f7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096724"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>サブスクリプションのアドオンを購入する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

既存のサブスクリプションにアドオンを購入する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- サブスクリプション ID。 これは、アドオンプランを購入するための既存のサブスクリプションです。

- 購入するアドオンプランを識別するプラン ID。

## <a name="purchasing-an-add-on-through-code"></a>コードを使用したアドオンの購入

サブスクリプションにアドオンを購入すると、そのアドオンの順序に従って元のサブスクリプションの順序が更新されます。 次の例では、customerId は顧客 ID、subscriptionId はサブスクリプション ID、addOnOfferId はアドオンのプラン ID です。

この手順を以下に示します。

1.  サブスクリプションの操作へのインターフェイスを取得します。

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  このインターフェイスを使用して、サブスクリプションオブジェクトをインスタンス化します。 これにより、注文 id を含む親サブスクリプションの詳細が取得されます。

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  新しい[**Order**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order)オブジェクトをインスタンス化します。 この注文インスタンスは、サブスクリプションの購入に使用された元の注文を更新するために使用されます。 アドオンを表す注文に1つの行項目を追加します。
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  サブスクリプションの元の注文をアドオンの新しい注文で更新します。
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

アドオンを購入するには、まずサブスクリプション操作へのインターフェイスを取得します。そのためには、顧客 ID を指定して ById メソッドを呼び出し、 [**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)プランを持つサブスクリプションを識別する[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)メソッドを呼び出します。 この[**インターフェイス**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription)を使用して、 [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get)を呼び出してサブスクリプションの詳細を取得します。 サブスクリプションの詳細が必要な理由 サブスクリプション注文の注文 id が必要であるためです。 これがアドオンで更新される順序です。

次に、次のコードスニペットに示すように、新しい[**Order**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order)オブジェクトをインスタンス化し、アドオンを識別するための情報を含む単一の[**LineItem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem)インスタンスを設定します。 この新しいオブジェクトを使用して、サブスクリプションの順序をアドオンで更新します。 最後に、Iaggregatepartner.customers を使用して顧客を特定し、 [**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)と[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)を使用して注文した後、 [**Patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch)メソッドを呼び出してサブスクリプションの順序を更新します。

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: AddSubscriptionAddOn.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法    | 要求 URI                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameters"></a>URI パラメーター

顧客と注文を識別するには、次のパラメーターを使用します。

| 名前                   | Type     | 必須 | 説明                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | この値は、顧客を識別する GUID 形式の**顧客テナント id**です。 |
| **注文-id**           | **guid** | Y        | 順序識別子。                                                              |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

次の表では、要求本文のプロパティについて説明します。

## <a name="order"></a>順番

| 名前                | Type             | 必須 | 説明                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | string           | N        | 注文 ID。                                        |
| ReferenceCustomerId | string           | Y        | 顧客 ID。                                     |
| LineItems           | オブジェクトの配列 | Y        | [Orderlineitem](#orderlineitem)オブジェクトの配列です。 |
| CreationDate        | string           | N        | 注文が作成された日付 (日付/時刻形式)。 |
| 属性          | object           | N        | "ObjectType": "Order" を格納します。                      |

## <a name="orderlineitem"></a>OrderLineItem

| 名前                 | Type   | 必須 | 説明                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber       | number | Y        | 0から始まる行項目番号。                       |
| OfferId              | string | Y        | アドオンのプラン ID。                                  |
| SubscriptionId       | string | N        | 購入したアドオンサブスクリプションの ID。                 |
| ParentSubscriptionId | string | Y        | アドオンが用意されている親サブスクリプションの ID。 |
| FriendlyName         | string | N        | この行項目の表示名。                        |
| Quantity             | number | Y        | ライセンスの数。                                      |
| PartnerIdOnRecord    | string | N        | レコードのパートナーの MPN ID。                         |
| 属性           | object | N        | "ObjectType": "OrderLineItem" が含まれています。                      |

### <a name="request-example"></a>要求の例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
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

成功した場合、このメソッドは応答本文で更新されたサブスクリプションの順序を返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "none",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```
