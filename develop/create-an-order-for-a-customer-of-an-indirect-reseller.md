---
title: Create an order for a customer of an indirect reseller
description: How to create an order for a customer of an indirect reseller.
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
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>Create an order for a customer of an indirect reseller

適用対象:

- パートナー センター

How to create an order for a customer of an indirect reseller.

## <a name="prerequisites"></a>前提条件

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
- The customer identifier.
- The offer identifier of the item to purchase.
- The tenant identifier of the indirect reseller.

## <a name="c"></a>C\#

To create an order for a customer of an indirect reseller:

1. Get a collection of the indirect resellers that have a relationship with the signed-in partner.
2. Get a local variable to the item in the collection that matches the indirect reseller ID. This step helps you access the reseller's [**MpnId**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) property when you create the order.
3. Instantiate an [**Order**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and set the [**ReferenceCustomerID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) property to the customer identifier in order to record the customer.
4. Create a list of [**OrderLineItem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objects, and assign the list to the order's [**LineItems**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) property. Each order line item contains the purchase information for one offer. Be sure to populate the [**PartnerIdOnRecord**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) property in each line item with the MPN ID of the indirect reseller. You must have at least one order line item.
5. Obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieve the interface from the [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.
6. Call the [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method to create the order.

### <a name="c-example"></a>C\# example

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

**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: PlaceOrderForCustomer.cs

## <a name="rest-request"></a>REST request

### <a name="request-syntax"></a>要求の構文

| メソッド   | 要求 URI                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

Use the following path parameter to identify the customer.

| 名前        | タスクバーの検索ボックスに   | 必須かどうか | 説明                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | [はい]      | A GUID formatted string that identifies the customer. |

### <a name="request-headers"></a>要求ヘッダー

See [Partner Center REST headers](headers.md) for more information.

### <a name="request-body"></a>要求本文

#### <a name="order"></a>[オーダー]

This table describes the **Order** properties in the request body.

| 名前 | タスクバーの検索ボックスに | 必須かどうか | 説明 |
| ---- | ---- | -------- | ----------- |
| id | string | 必須ではない | An order identifier that is supplied upon successful creation of the order. |
| referenceCustomerId | string | [はい] | The customer identifier. |
| billingCycle | string | 必須ではない | The frequency with which the partner is billed for this order. The default is &quot;Monthly&quot; and is applied upon successful creation of the order. Supported values are the member names found in [**BillingCycleType**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype). Note: the annual billing feature is not yet generally available. 年次請求のサポートは、間もなくご利用可能になります。 |
| lineItems | オブジェクトの配列 | [はい] | An array of [**OrderLineItem**](#orderlineitem) resources. |
| creationDate | string | 必須ではない | The date the order was created, in date-time format. Applied upon successful creation of the order. |
| 属性 | オブジェクト | 必須ではない | Contains "ObjectType": "Order". |

#### <a name="orderlineitem"></a>OrderLineItem

This table describes the **OrderLineItem** properties in the request body.

| 名前 | タスクバーの検索ボックスに | 必須かどうか | 説明 |
| ---- | ---- | -------- | ----------- |
| lineItemNumber | 整数 | [はい] | Each line item in the collection gets a unique line number, counting up from 0 to count-1. |
| offerId | string | [はい] | The offer identifier. |
| subscriptionId | string | 必須ではない | The subscription identifier. |
| parentSubscriptionId | string | 必須ではない | (省略可能)。 The ID of the parent subscription in an add-on offer. Applies to PATCH only. |
| friendlyName | string | 必須ではない | (省略可能)。 The friendly name for the subscription defined by the partner to help disambiguate. |
| quantity | 整数 | [はい] | The number of licenses for a license-based subscription. |
| partnerIdOnRecord | string | 必須ではない | When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider). This ensures proper accounting for incentives. **Failure to provide the reseller MPN ID does not cause the order to fail. However, the reseller is not recorded and as a consequence incentive calculations may not include the sale.** |
| 属性 | オブジェクト | 必須ではない | Contains "ObjectType":"OrderLineItem". |

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

## <a name="rest-response"></a>REST response

If successful, the response body contains the populated [Order](order-resources.md) resource.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

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