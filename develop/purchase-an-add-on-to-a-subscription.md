---
title: Purchase an add-on to a subscription
description: How to purchase an add-on to an existing subscription.
ms.assetid: 743520E5-0501-4403-B977-5E6D3E32DEC3
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e90aa545e2e1b76ccdb9f8e812df73d3113dfd86
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486752"
---
# <a name="span-idpc_apiv2purchase_an_add-on_to_a_subscriptionpurchase-an-add-on-to-a-subscription"></a><span id="pc_apiv2.purchase_an_add-on_to_a_subscription"/>Purchase an add-on to a subscription


**Applies To**

- パートナー センター
- 21Vianet が運営するパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

How to purchase an add-on to an existing subscription.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A customer ID (customer-tenant-id). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.
- A subscription ID. This is the existing subscription for which to purchase an add-on offer.
- An offer ID that identifies the add-on offer to purchase.

## <a name="span-idpurchasing_an_add-on_through_codespan-idpurchasing_an_add-on_through_codespan-idpurchasing_an_add-on_through_codepurchasing-an-add-on-through-code"></a><span id="Purchasing_an_add-on_through_code"/><span id="purchasing_an_add-on_through_code"/><span id="PURCHASING_AN_ADD-ON_THROUGH_CODE"/>Purchasing an add-on through code


When you purchase an add-on to a subscription you are updating the original subscription order with the order for the add-on. In the following, customerId is the customer ID, subscriptionId is the subscription ID, and addOnOfferId is the offer ID for the add-on.

Here are the steps:

1.  Get an interface to the operations for the subscription.
    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Use that interface to instantiate a subscription object. This gets you the parent subscription details, including the order id.
    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Instantiate a new [**Order**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order) object. This order instance is used to update the original order used to purchase the subscription. Add a single line item to the order that represents the add-on.
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

4.  Update the original order for the subscription with the new order for the add-on.
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


To purchase an add-on, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription that has the add-on offer. Use that [**interface**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get). Why do you need the subscription details? Because you need the order id of the subscription order. That's the order to be updated with the add-on.

Next, instantiate a new [**Order**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and populate it with a single [**LineItem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) instance that contains the information to identify the add-on, as shown in the following code snippet. You'll use this new object to update the subscription order with the add-on. Finally, call the [**Patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) method to update the subscription order, after first identifying the customer with [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) and the order with [**Orders.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).

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

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: AddSubscriptionAddOn.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>Request


**Request syntax**

| メソッド    | 要求 URI                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **PATCH** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

 

**URI parameters**

Use the following parameters to identify the customer and order.

| 名前                   | タスクバーの検索ボックスに     | 必須かどうか | 説明                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | The value is a GUID formatted **customer-tenant-id** that identifies the customer. |
| **order-id**           | **guid** | Y        | The order identifier.                                                              |

 

**Request headers**

See [Partner Center REST headers](headers.md) for more information.

**Request body**

The following tables describe the properties in the request body.

## <a name="span-idorderspan-idorderspan-idorderorder"></a><span id="Order"/><span id="order"/><span id="ORDER"/>Order


| 名前                | タスクバーの検索ボックスに             | 必須かどうか | 説明                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | string           | N        | The order ID.                                        |
| ReferenceCustomerId | string           | Y        | The customer ID.                                     |
| LineItems           | オブジェクトの配列 | Y        | An array of [OrderLineItem](#orderlineitem) objects. |
| CreationDate        | string           | N        | The date the order was created, in date-time format. |
| 属性          | オブジェクト           | N        | Contains "ObjectType": "Order".                      |

 

## <a name="span-idorderlineitemspan-idorderlineitemspan-idorderlineitemorderlineitem"></a><span id="orderLineItem"/><span id="orderlineitem"/><span id="ORDERLINEITEM"/>OrderLineItem


| 名前                 | タスクバーの検索ボックスに   | 必須かどうか | 説明                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber       | number | Y        | The line item number, starting with 0.                       |
| OfferId              | string | Y        | The offer ID of the add-on.                                  |
| SubscriptionId       | string | N        | The ID of the add-on subscription purchased.                 |
| ParentSubscriptionId | string | Y        | The ID of the parent subscription that has the add-on offer. |
| FriendlyName         | string | N        | The friendly name for this line item.                        |
| Quantity             | number | Y        | The number of licenses.                                      |
| PartnerIdOnRecord    | string | N        | The MPN ID of the partner of record.                         |
| 属性           | オブジェクト | N        | Contains "ObjectType": "OrderLineItem".                      |

 

**Request example**

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

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>Response


If successful, this method returns the updated subscription order in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center Error Codes](error-codes.md).

**Response example**

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

 

 




