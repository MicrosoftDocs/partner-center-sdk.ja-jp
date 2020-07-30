---
title: 統合サンドボックスから注文を取り消す
description: 統合サンドボックスアカウントから注文をキャンセルします。
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4bed678dc5f892dfe81d09daca820f24f177a91a
ms.sourcegitcommit: 68a5497a7350e135358aeb7f2a54c75707f922c5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87261911"
---
# <a name="cancel-an-order-from-the-integration-sandbox"></a>統合サンドボックスから注文を取り消す

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

統合サンドボックスアカウントから、予約済みのインスタンス、ソフトウェア、および商用 marketplace のサービスとしてのソフトウェア (SaaS) のサブスクリプションを取り消す方法。

>[!NOTE]
>予約されたインスタンスまたは商用 marketplace の SaaS サブスクリプションの注文は、統合サンドボックスアカウントからのキャンセルのみが可能であることに注意してください。  

API を通じてソフトウェアの製造注文をキャンセルするには、 [[キャンセル-ソフトウェアの購入]](cancel-software-purchases.md)を使用します。
[[購入のキャンセル]](https://docs.microsoft.com/partner-center/csp-software-subscriptions)を使用して、ダッシュボードを使用してソフトウェアの生産注文をキャンセルすることもできます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 統合サンドボックスパートナーアカウント。アクティブな予約インスタンス/ソフトウェア/サードパーティの SaaS サブスクリプション注文を持つ顧客がいます。

## <a name="c"></a>C\#

統合サンドボックスから注文を取り消すには、アカウントの資格情報をメソッドに渡して、 [**`CreatePartnerOperations`**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) [**`IPartner`**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner) パートナー操作を取得するためのインターフェイスを取得します。

特定の[順序](order-resources.md#order)を選択するには、パートナー操作を使用し、 [**`Customers.ById()`**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) 顧客識別子と共にメソッドを呼び出して顧客を指定します。次に、order 識別子を指定して **`Orders.ById()`** 順序と finally **`Get`** または **`GetAsync`** メソッドを取得する方法を指定します。

プロパティを [**`Order.Status`**](order-resources.md#order) に設定 `cancelled` し、メソッドを使用して順序を更新し **`Patch()`** ます。

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法     | 要求 URI                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

顧客を削除するには、次のクエリパラメーターを使用します。

| 名前                   | Type     | 必須 | 説明                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | この値は、リセラーがリセラーに属する特定の顧客の結果をフィルター処理できるようにする GUID 形式の**顧客テナント id**です。 |
| **注文-id** | **string** | Y        | 値は、キャンセルする必要がある注文 Id を示す文字列です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a>要求の例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは取り消された順序を返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
