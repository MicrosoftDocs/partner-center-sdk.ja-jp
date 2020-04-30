---
title: ID で注文を取得する
description: 顧客と注文 ID に一致する注文リソースを取得します。
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 164c2031f865a4ccc62d850263c066584d6214f6
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157744"
---
# <a name="get-an-order-by-id"></a>ID で注文を取得する

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

顧客と注文 ID に一致する[注文](order-resources.md)リソースを取得します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナーセンターの[ダッシュボード](https://partner.microsoft.com/dashboard)で確認できます。 パートナーセンターメニューの [ **CSP** ] を選択し、[ **Customers**] をクリックします。 [Customer] リストから顧客を選択し、[Account] \ (**アカウント**\) を選択します。 お客様のアカウントページで、[**お客様のアカウント情報**] セクションで**Microsoft ID**を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- 注文 ID。

## <a name="c"></a>C\#

顧客の注文を ID で取得するには、次のようにします。

1. **IAggregatePartner.Customers** コレクションを使用し、**ById()** メソッドを呼び出します。

2. [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)プロパティを呼び出し、それに続けて[**ByID ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)メソッドを呼び出します。
3. [**Get ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.get)または[**GetAsync ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync)を呼び出します。

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: partnersdk. FeatureSample**クラス**: GetOrder.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

顧客の注文を ID で取得するには、次のようにします。

1. **Iaggregatepartner.customers**関数を使用し、 **byId ()** 関数を呼び出します。

2. **Getorders**関数を呼び出し、その後に**byID ()** 関数を呼び出します。
3. **Get ()** 関数を呼び出します。

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

顧客の注文を ID で取得するには、 [**Get partnercustomer order**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md)コマンドを実行し、 **CustomerId**および**OrderId**パラメーターを指定します。

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1  |

#### <a name="uri-parameters"></a>URI パラメーター

次の表は、ID で注文を取得するために必要なクエリパラメーターを示しています。

| 名前                   | Type     | 必須 | 説明                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| customer-tenant-id     | string   | はい      | 顧客に対応する GUID 形式の文字列。 |
| id-for-order           | string   | はい      | 注文 ID に対応する文字列。                |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で[注文](order-resources.md)リソースを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 823
Content-Type: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Date: Thu, 15 Mar 2018 22:05:30 GMT

{
    "id": "YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
    "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol" : "$",
    "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "DZH318Z0BQ4Z:002L:DZH318Z0CMNP",
        "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_1_Year",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4Z/skus/002L?country=US",
                "method": "GET",
                "headers": []
            }
        }
    }
    ],
    "creationDate": "2018-03-13T22:49:54.3396949Z",
    "status": "completed",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
