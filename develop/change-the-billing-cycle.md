---
title: 請求サイクルを変更する
description: サブスクリプションを毎月または年間請求に更新します。
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3080ef40f71a043b4f02a7dc37178973d72aa09c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489022"
---
# <a name="change-the-billing-cycle"></a>請求サイクルを変更する

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

月単位、年単位、または月単位の請求に対して、[注文](order-resources.md)を更新します。

パートナーセンターのダッシュボードでは、顧客のサブスクリプションの詳細ページに移動することによって、この操作を実行できます。 この時点で、サブスクリプションの現在の請求サイクルを定義するオプションが表示され、サブスクリプションを変更して送信することができます。  

このトピックの**範囲外**:  

- 試用の請求サイクルの変更
- Azure サブスクリプション & 年間契約期間 (月単位、6年間) の請求サイクルの変更
- アクティブでないサブスクリプションの請求サイクルの変更
- Microsoft オンラインサービスライセンスベースのサブスクリプションの請求サイクルの変更

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客 ID (顧客-テナント id)。 顧客の ID を持っていない場合は、[顧客] リストから顧客を選択し、[アカウント] を選択して、Microsoft ID を保存することで、パートナーセンターで ID を検索できます。
- 注文 ID。

## <a name="c"></a>C#

請求サイクルの頻度を変更するには、[[**次数**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle?view=partnercenter-dotnet-latest#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle)] プロパティを更新します。

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド    | 要求 URI                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **KB830347** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次の表に、サブスクリプションの数量を変更するために必要なクエリパラメーターを示します。

| 名前                   | 種類 | 必須 | 説明                                                          |  
|------------------------|------|----------|----------------------------------------------------------------------|  
| **顧客-テナント id** | GUID |    Y     | 顧客を識別する GUID 形式の**顧客テナント id** |  
| **注文-id**           | GUID |    Y     | 順序識別子                                                 |  

### <a name="request-headers"></a>要求ヘッダー

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

次の表では、要求本文のプロパティについて説明します。

## <a name="order"></a>[オーダー]

| プロパティ           | 種類             | 必須 | 説明                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| ID                 | string           |    N     | 注文が正常に作成されたときに提供される注文 id |
|ReferenceCustomerId | string           |    Y     | 顧客識別子                                                    |
| 周期サイクル       | string           |    Y     | パートナーがこの注文に対して課金される頻度を示します。 サポートされている値は、 [BillingCycleType](product-resources.md#billingcycletype)で見つかったメンバー名です。 |
| LineItems          | オブジェクトの配列 |    Y     | [Orderlineitem](#orderlineitem)リソースの配列                      |
| CreationDate       | datetime         |    N     | 注文が作成された日付 (日付/時刻形式)                        |
| 属性         | オブジェクト           |    N     | "ObjectType": "OrderLineItem" が含まれています。                                     |

## <a name="orderlineitem"></a>OrderLineItem

| プロパティ             | 種類   | 必須 | 説明                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber       | number |    Y     | 0から始まる行項目番号。                                              |
| OfferId              | string |    Y     | プランの ID                                                                |
| SubscriptionId       | string |    Y     | サブスクリプションの ID                                                         |
| FriendlyName         | string |    N     | 明確に区別するためにパートナーによって定義されたサブスクリプションのフレンドリ名 |
| 数量             | number |    Y     | ライセンスまたはインスタンスの数                                                |
| PartnerIdOnRecord    | string |    N     | レコードのパートナーの MPN ID                                                |
| 属性           | オブジェクト |    N     | "ObjectType": "OrderLineItem" が含まれています。                                             |

### <a name="request-example"></a>要求の例

年間請求の更新

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
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
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

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

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
    "billingCycle": "Annual",
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
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
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