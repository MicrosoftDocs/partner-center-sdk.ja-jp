---
title: サブスクリプションにアドオンを購入する
description: 既存のサブスクリプションにアドオンを購入する方法。
ms.assetid: 743520E5-0501-4403-B977-5E6D3E32DEC3
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: f49685eb142945fc94e551e2113799c4c5b959e5
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416305"
---
# <a name="span-idpc_apiv2purchase_an_add-on_to_a_subscriptionpurchase-an-add-on-to-a-subscription"></a>サブスクリプションにアドオンを購入 <span id="pc_apiv2.purchase_an_add-on_to_a_subscription"/>には


**適用対象**

- Partner Center
- 21Vianet が運営するパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

既存のサブスクリプションにアドオンを購入する方法。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客 ID (顧客-テナント id)。 顧客の ID を持っていない場合は、[顧客] リストから顧客を選択し、[アカウント] を選択して、Microsoft ID を保存することで、パートナーセンターで ID を検索できます。
- サブスクリプション ID。 これは、アドオンプランを購入するための既存のサブスクリプションです。
- 購入するアドオンプランを識別するプラン ID。

## <a name="span-idpurchasing_an_add-on_through_codespan-idpurchasing_an_add-on_through_codespan-idpurchasing_an_add-on_through_codepurchasing-an-add-on-through-code"></a>コードを使用したアドオンの購入 <span id="PURCHASING_AN_ADD-ON_THROUGH_CODE"/><span id="purchasing_an_add-on_through_code"/>の <span id="Purchasing_an_add-on_through_code"/>


サブスクリプションにアドオンを購入すると、そのアドオンの順序に従って元のサブスクリプションの順序が更新されます。 次の例では、customerId は顧客 ID、subscriptionId はサブスクリプション ID、addOnOfferId はアドオンのプラン ID です。

手順は次のとおりです。

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

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


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

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求の構文**

| メソッド    | 要求 URI                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **KB830347** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

 

**URI パラメーター**

顧客と注文を識別するには、次のパラメーターを使用します。

| Name                   | 種類     | 必須 | 説明                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **顧客-テナント id** | **guid** | Y        | この値は、顧客を識別する GUID 形式の**顧客テナント id**です。 |
| **注文-id**           | **guid** | Y        | 順序識別子。                                                              |

 

**要求ヘッダー**

詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

次の表では、要求本文のプロパティについて説明します。

## <a name="span-idorderspan-idorderspan-idorderorder"></a><span id="Order"/><span id="order"/><span id="ORDER"/>の順序


| Name                | 種類             | 必須 | 説明                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | string           | N        | 注文 ID。                                        |
| referenceCustomerId | string           | Y        | 顧客 ID。                                     |
| lineItems           | オブジェクトの配列 | Y        | [Orderlineitem](#orderlineitem)オブジェクトの配列です。 |
| CreationDate        | string           | N        | 注文が作成された日付 (日付/時刻形式)。 |
| 属性          | object           | N        | "ObjectType": "Order" を格納します。                      |

 

## <a name="span-idorderlineitemspan-idorderlineitemspan-idorderlineitemorderlineitem"></a><span id="orderLineItem"/><span id="orderlineitem"/><span id="ORDERLINEITEM"/>OrderLineItem


| Name                 | 種類   | 必須 | 説明                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| lineItemNumber       | number | Y        | 0から始まる行項目番号。                       |
| OfferId              | string | Y        | アドオンのプラン ID。                                  |
| SubscriptionId       | string | N        | 購入したアドオンサブスクリプションの ID。                 |
| parentSubscriptionId | string | Y        | アドオンが用意されている親サブスクリプションの ID。 |
| FriendlyName         | string | N        | この行項目の表示名。                        |
| 数量             | number | Y        | ライセンスの数。                                      |
| partnerIdOnRecord    | string | N        | レコードのパートナーの MPN ID。                         |
| 属性           | object | N        | "ObjectType": "OrderLineItem" が含まれています。                      |

 

**要求の例**

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

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答


成功した場合、このメソッドは応答本文で更新されたサブスクリプションの順序を返します。

**応答成功およびエラーコード**

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

**応答の例**

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

 

 




