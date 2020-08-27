---
title: 注文を作成する
description: 顧客の注文を作成する方法。
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d92c117d4fb29ec054302cbc9dfa21214135d086
ms.sourcegitcommit: a8fe6268fed2162843e7c92dca41c3919b25647d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88937932"
---
# <a name="create-an-order"></a>注文を作成する

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**Azure 予約 VM インスタンス製品の注文の**作成は、次の*場合にのみ*適用されます。

- パートナー センター

現在販売可能なものの詳細については、 [Cloud Solution Provider プログラムのパートナープランに](https://docs.microsoft.com/partner-center/csp-offers)関する情報を参照してください。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- プラン識別子。

## <a name="c"></a>C\#

顧客の注文を作成するには、次のようにします。

1. [**注文**](order-resources.md)オブジェクトをインスタンス化し、 **ReferenceCustomerID**プロパティを顧客 ID に設定して顧客を記録します。

2. [**Orderlineitem**](order-resources.md#orderlineitem)オブジェクトの一覧を作成し、そのリストを注文の**LineItems**プロパティに割り当てます。 各注文品目には 1 つのプランの購入情報が含まれています。 少なくとも 1 つの注文品目が必要です。

3. 順序付け操作のためのインターフェイスを取得します。 まず、顧客 ID を指定して [**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) メソッドを呼び出し、顧客を識別します。 次に、 [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) プロパティからインターフェイスを取得します。

4. [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create)または[**createasync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync)メソッドを呼び出し、 [**Order**](order-resources.md)オブジェクトを渡します。

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**サンプル**: [コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル **クラス**: CreateOrder.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法   | 要求 URI                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

次のパス パラメーターを使用して顧客を指定します。

| Name        | 種類   | 必須 | 説明                                                |
|-------------|--------|----------|------------------------------------------------------------|
| customer-id | string | はい      | 顧客を識別する GUID 形式の顧客 id。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

#### <a name="order"></a>Order

次の表では、要求本文の [Order](order-resources.md) プロパティについて説明します。

| プロパティ             | 種類                        | 必須                        | 説明                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| id                   | string                      | いいえ                              | 注文が正常に作成されたときに提供される注文 id。   |
| referenceCustomerId  | string                      | いいえ                              | 顧客 ID。 |
| billingCycle         | string                      | いいえ                              | パートナーがこの注文に対して課金される頻度を示します。 サポートされる値は、[BillingCycleType](product-resources.md#billingcycletype) で検出されたメンバー名です。 既定値は、注文の作成時に "毎月" または "OneTime" です。 このフィールドは、注文が正常に作成されたときに適用されます。 |
| lineItems            | [Orderlineitem](order-resources.md#orderlineitem)リソースの配列 | はい      | 顧客が購入しているプランの一覧 (数量を含む)。        |
| currencyCode         | string                      | いいえ                              | 読み取り専用。 注文を配置するときに使用する通貨。 注文が正常に作成されたときに適用されます。           |
| creationDate         | DATETIME                    | いいえ                              | 読み取り専用。 注文が作成された日付 (日付/時刻形式)。 注文が正常に作成されたときに適用されます。                                   |
| status               | string                      | いいえ                              | 読み取り専用。 注文の状態。  サポートされる値は、 [Orderstatus](order-resources.md#orderstatus)で見つかったメンバー名です。        |
| リンク                | [OrderLinks](utility-resources.md#resourcelinks)              | いいえ                              | 注文に対応するリソースリンク。 |
| 属性           | [ResourceAttributes](utility-resources.md#resourceattributes) | いいえ                              | 順序に対応するメタデータ属性。 |

#### <a name="orderlineitem"></a>OrderLineItem

次の表では、要求本文の [Orderlineitem](order-resources.md#orderlineitem) プロパティについて説明します。

>[!NOTE]
>PartnerIdOnRecord は、間接リセラーが間接リセラーの代わりに注文を行う場合にのみ指定する必要があります。 間接リセラーの Microsoft Partner Network ID のみを格納するために使用されます (間接プロバイダーの ID ではありません)。

| Name                 | 種類   | 必須 | 説明                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | INT    | はい      | コレクション内の各品目には、0 からカウント -1 までカウントする、一意の品目番号が与えられます。                                                                                                                                                 |
| offerId              | string | はい      | プラン ID。                                                                                                                                                                                                                      |
| subscriptionId       | string | いいえ       | サブスクリプションの識別子です。                                                                                                                                                                                                               |
| parentSubscriptionId | string | いいえ       | 省略可能。 アドオン オファーの親サブスクリプションの ID。 PATCH にのみ適用されます。                                                                                                                                                     |
| friendlyName         | string | いいえ       | 省略可能。 明確に区別するためにパートナーによって定義されたサブスクリプションのフレンドリ名。                                                                                                                                              |
| 数量             | INT    | はい      | ライセンス ベースのサブスクリプションのライセンス数。                                                                                                                                                                                   |
| partnerIdOnRecord    | string | いいえ       | 間接プロバイダーが間接リセラーの代わりに注文を行う場合は、このフィールドに **間接リセラー** の MPN id のみを入力します (間接プロバイダーの id は使用しないでください)。 これにより、インセンティブを正しく計算できます。 |
| provisioningContext  | Dictionary<string、string>                | いいえ       |  カタログ内の一部の項目のプロビジョニングに必要な情報。 SKU の "プロビジョニング変数" プロパティは、カタログ内の特定のアイテムに必要なプロパティを示します。                  |
| リンク                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | いいえ       |  読み取り専用。 注文明細項目に対応するリソースリンク。  |
| 属性           | [ResourceAttributes](utility-resources.md#resourceattributes) | いいえ       | OrderLineItem に対応するメタデータ属性。 |
| renewsTo             | オブジェクトの配列                          | いいえ    |[Renewsto](order-resources.md#renewsto)の配列。                                                                            |

##### <a name="renewsto"></a>RenewsTo

次の表では、要求本文の [renewsto](order-resources.md#renewsto) について説明します。

| プロパティ              | 種類             | 必須        | 説明 |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | string           | いいえ              | 更新用語の期間の ISO 8601 表現。 現在サポートされている値は、 **P1M** (1 か月) と **P1Y** (1 年) です。 |

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、メソッドは応答本文で [注文](order-resources.md) リソースを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「 [パートナーセンターのエラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
