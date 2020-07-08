---
title: カートを作成する
description: 買い物かごに顧客の注文を追加する方法。
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: aa3bd159a850028a30ee88edc22bb3b263df310e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096326"
---
# <a name="create-a-cart"></a>カートを作成する

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

買い物かごに顧客の注文を追加することができます。 現在販売可能なものの詳細については、 [Cloud Solution Provider プログラムのパートナープランに](https://docs.microsoft.com/partner-center/csp-offers)関する情報を参照してください。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="c"></a>C\#

顧客の注文を作成するには、次のようにします。

1. カートオブジェクトをインスタンス化します。

2. **CartLineItem**オブジェクトの一覧を作成し、そのリストをカートの LineItems プロパティに割り当てます。 各カートの品目には、1つの製品の購入情報が含まれています。 少なくとも1つのカート品目が必要です。

3. 顧客 ID を指定して**ById**メソッドを呼び出して顧客を識別し、**カート**プロパティからインターフェイスを取得することによって、カート操作へのインターフェイスを取得します。

4. カートを作成するには、 **create**または**createasync**メソッドを呼び出します。

### <a name="c-example"></a>C の \# 例

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

var cart = new Cart()
{
    LineItems = new List<CartLineItem>()
    {
        new CartLineItem()
        {
      /* Microsoft Azure Subscription */
            Id = 0,
            CatalogItemId = "MS-AZR-0145P",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1Y"
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 1,
            CatalogItemId = "DZH318Z0BQ36:004G:DZH318Z08C0S",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P1Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 2,
            CatalogItemId = "DZH318Z0BQ36:004J:DZH318Z08B8X",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P3Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Perpetual Software */
            Id = 3,
            CatalogItemId = "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime
        },
        new CartLineItem()
        {
      /* SaaS */
            Id = 4,
            CatalogItemId = "DZH318Z0BXWC:0002:DZH318Z0BMRV",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1M"
        },
        new CartLineItem()
        {
      /* SaaS Free Trial */
            Id = 5,
            CatalogItemId = "DZH318Z0C0WF:0001:DZH318Z0BP69",
            Quantity = 10,
            BillingCycle = BillingCycleType.None,
            TermDuration = "P1M",
            RenewsTo = new RenewsTo
            {
                TermDuration = "P1Y"
            }
        }
    }
};

cart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

顧客の注文を作成するには、次のようにします。

1. カートオブジェクトをインスタンス化します。

2. **CartLineItem**オブジェクトの一覧を作成し、そのリストをカートの品目に割り当てます。 各カートの品目には、1つの製品の購入情報が含まれています。 少なくとも1つのカート品目が必要です。

3. 顧客 ID を指定して**iaggregatepartner.customers () byId**関数を呼び出して顧客を識別し、 **getcustomers**関数からインターフェイスを取得することによって、カート操作へのインターフェイスを取得します。

4. カートを作成するには、 **create**関数を呼び出します。

## <a name="java-example"></a>Java の例

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;
// String catalogItemId;

CartLineItem lineItem = new CartLineItem();

lineItem.setBillingCycle(BillingCycleType.OneTime);
lineItem.setCatalogItemId(catalogItemId);
lineItem.setFriendlyName("Sample RI Purchase");
lineItem.setQuantity(1);

Map<String, String> provisioningContext = new HashMap<String,String>();

provisioningContext.put("duration", "3Years");
provisioningContext.put("scope", "shared");
provisioningContext.put("subscriptionId", subscriptionId);

lineItem.setProvisioningContext(provisioningContext);

List<CartLineItem> lineItemList = new ArrayList<CartLineItem>();
lineItemList.add(lineItem);

Cart cart = new Cart();
cart.setLineItems(lineItemList);

Cart cartCreated = partnerOperations.getCustomers().byId(customerId).getCarts().create(cart);
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

顧客の注文を作成するには、次のようにします。

1. カートオブジェクトをインスタンス化します。

2. **CartLineItem**オブジェクトの一覧を作成し、そのリストをカートの品目に割り当てます。 各カートの品目には、1つの製品の購入情報が含まれています。 少なくとも1つのカート品目が必要です。

3. [**新しい-Partner顧客カート**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md)コマンドを実行して、カートを作成します。

```powershell
# $customerId
# $subscriptionId
# $catalogItemId

$lineItem = New-Object -TypeName Microsoft.Store.PartnerCenter.PowerShell.Models.Carts.PSCartLineItem

$lineItem.BillingCycle = 'OneTime'
$lineItem.CatalogItemId = $catalogItemId
$lineItem.FriendlyName = 'Sample RI Purchase'
$lineItem.ProvisioningContext.Add('duration', '1Year')
$lineItem.ProvisioningContext.Add('scope', 'shared')
$lineItem.ProvisioningContext.Add('subscriptionId', $subsciptionId)
$lineItem.Quantity = 10

New-PartnerCustomerCart -CustomerId $customerId -LineItems $lineItem
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法   | 要求 URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1                        |

### <a name="uri-parameter"></a>URI パラメーター

次のパス パラメーターを使用して顧客を指定します。

| 名前            | Type     | 必須 | 説明                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **顧客 id** | string   | はい      | 顧客を識別する GUID 形式の顧客 id。             |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

次の表では、要求本文に含まれる[カート](cart-resources.md)のプロパティについて説明します。

| プロパティ              | Type             | 必須        | 説明 |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | string           | いいえ              | カートが正常に作成されたときに提供されるカート識別子。                                  |
| 前のタイムスタンプ     | DateTime         | いいえ              | カートが作成された日付 (日付/時刻形式)。 カートが正常に作成されたときに適用されます。         |
| lastModifiedTimeStamp | DateTime         | いいえ              | カートが最後に更新された日付 (日付/時刻形式)。 カートが正常に作成されたときに適用されます。    |
| expirationTimeStamp   | DateTime         | いいえ              | カートの有効期限が切れる日付 (日付と時刻の形式)。  カートの作成が成功したときに適用されます。            |
| lastModifiedUser      | 文字列           | いいえ              | カートを最後に更新したユーザー。 カートの作成が成功したときに適用されます。                             |
| lineItems             | オブジェクトの配列 | はい             | [CartLineItem](cart-resources.md#cartlineitem)リソースの配列。                                     |

次の表では、要求本文の[CartLineItem](cart-resources.md#cartlineitem)プロパティについて説明します。

|      プロパティ       |            Type             | 必須 |                                                                                         説明                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         id          |           string            |    いいえ    |                                                     カートの品目の一意の識別子。 カートの作成が成功したときに適用されます。                                                     |
|      catalogId      |           string            |   はい    |                                                                                カタログ項目の識別子。                                                                                 |
|    friendlyName     |           文字列            |    いいえ    |                                                    省略可能。 明確に区別できるように、パートナーによって定義された項目のフレンドリ名。                                                    |
|      数量       |             INT             |   はい    |                                                                            ライセンスまたはインスタンスの数。                                                                             |
|    currencyCode     |           文字列            |    いいえ    |                                                                                     通貨コード。                                                                                      |
|    billingCycle     |           Object            |   はい    |                                                                    現在の期間に設定されている請求サイクルの種類。                                                                    |
|    participants     | オブジェクトの文字列ペアの一覧 |    いいえ    |                                                                購入時のレコードの PartnerId (MPNID) のコレクション。                                                                 |
| provisioningContext | Dictionary<string、string>  |    いいえ    | カタログ内の一部の項目のプロビジョニングに必要な情報。 SKU の "プロビジョニング変数" プロパティは、カタログ内の特定のアイテムに必要なプロパティを示します。 |
|     orderGroup      |           文字列            |    いいえ    |                                                                   一緒に配置できる項目を示すグループ。                                                                   |
|        エラー        |           Object            |    いいえ    |                                                                     エラーが発生した場合にカートが作成された後に適用されます。                                                                      |
|     renewsTo        | オブジェクトの配列            |    いいえ    |                                                    [Renewsto](cart-resources.md#renewsto)の配列。                                                                            |

次の表では、要求本文の[renewsto](cart-resources.md#renewsto)について説明します。

| プロパティ              | Type             | 必須        | 説明 |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | 文字列           | いいえ              | 更新用語の期間の ISO 8601 表現。 現在サポートされている値は、 **P1M** (1 か月) と**P1Y** (1 年) です。 |

### <a name="request-example"></a>要求の例

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
  "lineItems": [
    {
    /* Microsoft Azure Subscription */
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1Y"
    },
    {
    /* Azure Reserved Instance */
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      }
    },
    {
    /* Azure Reserved Instance */
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "single"
      }
    },
    {
    /* Perpetual Software */
      "id": 3,
      "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSFM",
      "quantity": 1,
      "billingCycle": "one_time"
    },
    {
    /* SaaS */
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1M"
    },
  {
    /* SaaS Free Trial */
       "id": 5,
       "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
       "quantity": 10,
       "billingCycle": "none",
       "termDuration": "P1M",
       "renewsTo": {
         "termDuration": "P1Y"
       }
    }
  ]
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは、応答本文で設定された[カート](cart-resources.md)リソースを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
  "id": "3655b1a0-b1c9-4268-9824-577fdbc4d0be",
  "creationTimestamp": "2019-01-16T00:45:41.6062996Z",
  "lastModifiedTimestamp": "2019-01-16T00:45:41.6062996Z",
  "expirationTimestamp": "2019-01-16T01:00:54.4188497Z",
  "lastModifiedUser": "1824b7fc-2fac-4478-b177-66823c40ab75",
  "status": "Active",
  "lineItems": [
    {
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1Y",
      "orderGroup": "OMS-0"
    },
    {
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 3,
      "catalogItemId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "orderGroup": "0"
    },
    {
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1M",
      "orderGroup": "1"
    },
  {
      "id": 5,
      "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
      "quantity": 10,
      "currencyCode": "USD",
      "billingCycle": "none",
      "termDuration": "P1M",
      "renewsTo": {
  "termDuration": "P1Y"
      },
    "orderGroup": "2"
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/28045616-f6b9-462f-9701-0d89b5e65c44/carts/3655b1a0-b1c9-4268-9824-577fdbc4d0be",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Cart"
  }
}
```
