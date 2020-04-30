---
title: カートを更新する
description: カート内の顧客の注文を更新する方法。
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: f6e0a54f088c3e1ecbc00338e67a143b655b708e
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157644"
---
# <a name="update-a-cart"></a>カートを更新する

**適用対象**

- パートナー センター

カート内の顧客の注文を更新する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナーセンターの[ダッシュボード](https://partner.microsoft.com/dashboard)で確認できます。 パートナーセンターメニューの [ **CSP** ] を選択し、[ **Customers**] をクリックします。 [Customer] リストから顧客を選択し、[Account] \ (**アカウント**\) を選択します。 お客様のアカウントページで、[**お客様のアカウント情報**] セクションで**Microsoft ID**を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- 既存のカートのカート ID。

## <a name="c"></a>C\#

顧客の注文を更新するには、 **ById ()** 関数を使用して customer および cart ID を渡すことによって、 **get ()** メソッドを使用してカートを取得します。 カートに必要な変更を加えます。 次に、 **ById ()** メソッドを使用して、customer および cart ID を使用して**Put**メソッドを呼び出します。

最後に、 **Put ()** メソッドまたは**putasync ()** メソッドを呼び出して、注文を作成します。

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1              |

### <a name="uri-parameters"></a>URI パラメーター

次のパスパラメーターを使用して顧客を特定し、更新するカートを指定します。

| 名前            | Type     | 必須 | 説明                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **顧客 id** | string   | はい      | 顧客を識別する GUID 形式の顧客 id。             |
| **カート-id**     | string   | はい      | カートを識別する GUID 形式のカート id。                     |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

次の表では、要求本文に含まれる[カート](cart-resources.md)のプロパティについて説明します。

| プロパティ              | Type             | 必須        | 説明                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | string           | いいえ              | カートが正常に作成されたときに提供されるカート識別子。                                  |
| 前のタイムスタンプ     | DateTime         | いいえ              | カートが作成された日付 (日付/時刻形式)。 カートが正常に作成されたときに適用されます。        |
| lastModifiedTimeStamp | DateTime         | いいえ              | カートが最後に更新された日付 (日付/時刻形式)。 カートが正常に作成されたときに適用されます。    |
| expirationTimeStamp   | DateTime         | いいえ              | カートの有効期限が切れる日付 (日付と時刻の形式)。  カートの作成が成功したときに適用されます。            |
| lastModifiedUser      | string           | いいえ              | カートを最後に更新したユーザー。 カートの作成が成功したときに適用されます。                             |
| lineItems             | オブジェクトの配列 | はい             | [CartLineItem](cart-resources.md#cartlineitem)リソースの配列。                                               |

次の表では、要求本文の[CartLineItem](cart-resources.md#cartlineitem)プロパティについて説明します。

| プロパティ             | Type                        | 必須     | 説明                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | string                      | いいえ           | カートの品目の一意の識別子。 カートの作成が成功したときに適用されます。                |
| catalogId            | string                      | はい          | カタログ項目の識別子。                                                                       |
| friendlyName         | string                      | いいえ           | 省略可能。 明確に区別できるように、パートナーによって定義された項目のフレンドリ名。              |
| 数量             | INT                         | はい          | ライセンスまたはインスタンスの数。     |
| currencyCode         | string                      | いいえ           | 通貨コード。                                                                                 |
| billingCycle         | Object                      | はい          | 現在の期間に設定されている請求サイクルの種類。                                              |
| participants         | オブジェクトの文字列ペアの一覧 | いいえ           | 購入の参加者のコレクション。                                                      |
| provisioningContext  | Dictionary<string、string>  | いいえ           | プランのプロビジョニングに使用されるコンテキスト。                                                          |
| orderGroup           | string                      | いいえ           | 一緒に配置できる項目を示すグループ。                                            |
| error                | Object                      | いいえ           | エラーが発生した場合にカートが作成された後に適用されます。                                                 |

### <a name="request-example"></a>要求の例

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
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
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
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
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```
