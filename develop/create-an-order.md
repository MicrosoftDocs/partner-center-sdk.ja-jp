---
title: 注文を作成する
description: 顧客の注文を作成する方法。
ms.assetid: FE4949FA-7C4D-462D-8F32-FAADCF166875
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7600ab546f7bcde0e8c01c3216949bcfef290b1d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489662"
---
# <a name="create-an-order"></a>注文を作成する

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**Azure 予約 VM インスタンス製品の注文の**作成は、次の*場合にのみ*適用されます。

- パートナー センター

現在販売可能なものの詳細については、 [Cloud Solution Provider プログラムのパートナープランに](https://docs.microsoft.com/partner-center/csp-offers)関する情報を参照してください。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客識別子。
- プラン識別子。

## <a name="c"></a>C\#

顧客の注文を作成するには、次のようにします。

1. [**注文**](order-resources.md)オブジェクトをインスタンス化し、 **ReferenceCustomerID**プロパティを顧客 ID に設定して顧客を記録します。
2. [**Orderlineitem**](order-resources.md#orderlineitem)オブジェクトの一覧を作成し、そのリストを注文の**LineItems**プロパティに割り当てます。 各注文品目には、1つのオファーの購入情報が含まれています。 少なくとも1つの注文品目が必要です。
3. 順序付け操作のためのインターフェイスを取得します。 まず、顧客 ID を指定して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出し、顧客を識別します。 次に、 [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)プロパティからインターフェイスを取得します。
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

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: CreateOrder.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド   | 要求 URI                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **投稿** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

顧客を識別するには、次のパスパラメーターを使用します。

| 名前        | 種類   | 必須 | 説明                                                |
|-------------|--------|----------|------------------------------------------------------------|
| 顧客 id | string | 〇      | 顧客を識別する GUID 形式の顧客 id。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

#### <a name="order"></a>[オーダー]

次の表では、要求本文の[Order](order-resources.md)プロパティについて説明します。

| プロパティ             | 種類                        | 必須                        | 説明                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| id                   | string                      | X                              | 注文が正常に作成されたときに提供される注文 id。   |
| ReferenceCustomerId  | string                      | X                              | 顧客識別子。 |
| 周期サイクル         | string                      | X                              | パートナーがこの注文に対して課金される頻度を示します。 サポートされている値は、 [BillingCycleType](product-resources.md#billingcycletype)で見つかったメンバー名です。 既定値は、注文の作成時に "毎月" または "OneTime" です。 このフィールドは、注文が正常に作成されたときに適用されます。 |
| lineItems            | [Orderlineitem](order-resources.md#orderlineitem)リソースの配列 | 〇      | 顧客が購入しているプランの一覧 (数量を含む)。        |
| currencyCode         | string                      | X                              | 読み取り専用。 注文を配置するときに使用する通貨。 注文が正常に作成されたときに適用されます。           |
| CreationDate         | datetime                    | X                              | 読み取り専用。 注文が作成された日付 (日付/時刻形式)。 注文が正常に作成されたときに適用されます。                                   |
| status               | string                      | X                              | 読み取り専用。 注文の状態。  サポートされる値は、 [Orderstatus](order-resources.md#orderstatus)で見つかったメンバー名です。        |
| links                | [OrderLinks](utility-resources.md#resourcelinks)              | X                              | 注文に対応するリソースリンク。 |
| 属性           | [ResourceAttributes](utility-resources.md#resourceattributes) | X                              | 順序に対応するメタデータ属性。 |

#### <a name="orderlineitem"></a>OrderLineItem

次の表では、要求本文の[Orderlineitem](order-resources.md#orderlineitem)プロパティについて説明します。

>[!NOTE]
>PartnerIdOnRecord は、間接リセラーが間接リセラーの代わりに注文を行う場合にのみ指定する必要があります。 間接リセラーの Microsoft Partner Network ID のみを格納するために使用されます (間接プロバイダーの ID ではありません)。

| 名前                 | 種類   | 必須 | 説明                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| LineItemNumber       | int    | 〇      | コレクション内の各行項目は、0からカウント-1 までカウントされる一意の行番号を取得します。                                                                                                                                                 |
| offerId              | string | 〇      | プランの識別子。                                                                                                                                                                                                                      |
| subscriptionId       | string | X       | サブスクリプション識別子。                                                                                                                                                                                                               |
| ParentSubscriptionId | string | X       | (省略可能)。 アドオンプランの親サブスクリプションの ID。 PATCH にのみ適用されます。                                                                                                                                                     |
| friendlyName         | string | X       | (省略可能)。 明確に区別するためにパートナーによって定義されたサブスクリプションのフレンドリ名。                                                                                                                                              |
| quantity             | int    | 〇      | ライセンスベースのサブスクリプションのライセンス数。                                                                                                                                                                                   |
| PartnerIdOnRecord    | string | X       | 間接プロバイダーが間接リセラーの代わりに注文を行う場合は、このフィールドに**間接リセラー**の MPN id のみを入力します (間接プロバイダーの id は使用しないでください)。 これにより、インセンティブを適切にアカウンティングできます。 |
| provisioningContext  | Dictionary < string、string >                | X       |  カタログ内の一部の項目のプロビジョニングに必要な情報。 SKU の "プロビジョニング変数" プロパティは、カタログ内の特定のアイテムに必要なプロパティを示します。                  |
| links                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | X       |  読み取り専用。 注文明細項目に対応するリソースリンク。  |
| 属性           | [ResourceAttributes](utility-resources.md#resourceattributes) | X       | OrderLineItem に対応するメタデータ属性。 |
| RenewsTo             | オブジェクトの配列                          | X    |[Renewsto](order-resources.md#renewsto)の配列。                                                                            |

##### <a name="renewsto"></a>RenewsTo

次の表では、要求本文の[renewsto](order-resources.md#renewsto)について説明します。

| プロパティ              | 種類             | 必須        | 説明 |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | string           | X              | 更新用語の期間の ISO 8601 表現。 現在サポートされている値は、 **P1M** (1 か月) と**P1Y** (1 年) です。 |

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

成功した場合、メソッドは応答本文で[注文](order-resources.md)リソースを返します。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

このメソッドは、次のエラーコードを返します。

| HTTP 状態コード     | エラー コード   | 説明                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 400                  | 2093         | 選択されたカタログ項目では、インベントリを利用できません。                                                 |
| 400                  | 2094         | サブスクリプションは有効な Azure サブスクリプションではありません。 Azure 予約 VM インスタンスの購入にのみ適用されます。     |
| 400                  | 2095         | サブスクリプションは、Azure 予約 VM インスタンスの購入に対して有効になっていません。 |

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
    ],
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