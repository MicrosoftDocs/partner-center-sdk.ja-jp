---
title: アドオンを扱うカートを作成する
description: カート内の顧客のアドオンを含む注文を追加する方法。
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: rbars
ms.author: rbars
ms.openlocfilehash: 63dd12725ae488b6676077fe3a646551b793be73
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022679"
---
# <a name="create-a-cart-with-add-ons"></a>アドオンを扱うカートを作成する

**適用対象:**

- パートナー センター

カートを通じてアドオンを購入できます。 現在販売可能なものの詳細については、 [Cloud Solution Provider プログラムのパートナープランに](https://docs.microsoft.com/partner-center/csp-offers)関する情報を参照してください。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="c"></a>C\#

カートでは、基本プランとそれに対応するアドオンを購入できます。 カートを作成するには、次の手順に従います。

1. [**カート**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.carts.cart)オブジェクトをインスタンス化します。

2. 基本プランを表す[**CartLineItem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem)オブジェクトの一覧を作成し、そのリストをカートの[**LineItems**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems)プロパティに割り当てます。

3. 各基本プランのカート明細項目の下で、 **AddOnItems**の一覧に、その基本プランに対して購入されるアドオンを表す他の**CartLineItem**オブジェクトを入力します。

4. [**Iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.iaggregatepartner)を使用して買い物かご操作へのインターフェイスを取得し、顧客 ID を指定して[**ICustomerCollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出して顧客を識別し、**買い物かご**プロパティからインターフェイスを取得します。

5. 最後に、 [**create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create)または[**createasync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync)メソッドを呼び出してカートを作成します。

### <a name="c-example"></a>C の \# 例

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

次の手順に従ってカートを作成します。これにより、既存の基本サブスクリプションに対してアドオンを購入できます。

1. キー "ParentSubscriptionId" を使用して、 **ProvisioningContext**プロパティにサブスクリプション ID を含む新しい**CartLineItem**を使用して**カート**を作成します。

2. **Create**メソッドまたは**createasync**メソッドを呼び出します。

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法   | 要求 URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1                        |

#### <a name="uri-parameter"></a>URI パラメーター

次のパス パラメーターを使用して顧客を指定します。

| 名前            | 種類     | 必須 | 説明                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **顧客 id** | string   | はい      | 顧客を識別する GUID 形式の顧客 id。             |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

次の表では、要求本文に含まれる[カート](cart-resources.md)のプロパティについて説明します。

| プロパティ              | 種類             | 必須        | 説明 |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | string           | いいえ              | カートが正常に作成されたときに提供されるカート識別子。                                  |
| 前のタイムスタンプ     | DateTime         | いいえ              | カートが作成された日付 (日付/時刻形式)。 カートが正常に作成されたときに適用されます。         |
| lastModifiedTimeStamp | DateTime         | いいえ              | カートが最後に更新された日付 (日付/時刻形式)。 カートが正常に作成されたときに適用されます。    |
| expirationTimeStamp   | DateTime         | いいえ              | カートの有効期限が切れる日付 (日付と時刻の形式)。  カートの作成が成功したときに適用されます。            |
| lastModifiedUser      | 文字列           | いいえ              | カートを最後に更新したユーザー。 カートの作成が成功したときに適用されます。                             |
| lineItems             | オブジェクトの配列 | はい             | [CartLineItem](cart-resources.md#cartlineitem)リソースの配列。                                             |

次の表では、要求本文の[CartLineItem](cart-resources.md#cartlineitem)プロパティについて説明します。

| プロパティ             | 種類                             | 説明                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | string                           | カートの品目の一意の識別子。 カートの作成が成功したときに適用されます。                                                                   |
| catalogId            | string                           | カタログ項目の識別子。                                                                                                                          |
| friendlyName         | string                           | 省略可能。 明確に区別できるように、パートナーによって定義された項目のフレンドリ名。                                                                 |
| 数量             | INT                              | ライセンスまたはインスタンスの数。                                                                                                                  |
| currencyCode         | string                           | 通貨コード。                                                                                                                                    |
| billingCycle         | Object                           | 現在の期間に設定されている請求サイクルの種類。                                                                                                 |
| participants         | オブジェクトの文字列ペアの一覧      | 購入時のレコードの PartnerId (MPNID) のコレクション。                                                                                          |
| provisioningContext  | Dictionary<string、string>       | プランのプロビジョニングに使用されるコンテキスト。                                                                                                             |
| orderGroup           | string                           | 一緒に配置できる項目を示すグループ。                                                                                               |
| addonItems           | **CartLineItem**オブジェクトの一覧 | 親のカートの品目の購入から得られる基本サブスクリプションに対して購入されるアドオンのカート品目のコレクション。 |
| エラー                | Object                           | エラーが発生した場合にカートが作成された後に適用されます。                                                                                                    |

### <a name="request-example-new-base-subscription"></a>要求の例 (新しい基本サブスクリプション)

次の REST の例は、新しい基本サブスクリプションのアドオン項目を含むカートを作成する方法を示しています。

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a>要求の例 (既存の基本サブスクリプション)

次の REST の例は、既存の基本サブスクリプションにアドオンを追加する方法を示しています。

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは、応答本文で設定された[カート](cart-resources.md)リソースを返します。

#### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

#### <a name="response-example-new-base-subscription"></a>応答の例 (新しい基本サブスクリプション)

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a>応答の例 (既存の基本サブスクリプション)

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
