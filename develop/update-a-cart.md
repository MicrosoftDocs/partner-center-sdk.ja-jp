---
title: カートを更新する
description: カート内の顧客の注文を更新する方法。
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 70e20f1261f29468c5b0b7e017f29f6e64b91cf6
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487952"
---
# <a name="update-a-cart"></a>カートを更新する


**適用対象**

- パートナー センター


カート内の顧客の注文を更新する方法。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客識別子。 顧客の ID を持っていない場合は、[顧客] リストから顧客を選択し、[アカウント] を選択して、Microsoft ID を保存することで、パートナーセンターで ID を検索できます。
- 既存のカートのカート ID。


## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


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

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求


**要求の構文**

| メソッド  | 要求 URI                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **投入** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1              |

 

**URI パラメーター**

次のパスパラメーターを使用して顧客を特定し、更新するカートを指定します。

| 名前            | 種類     | 必須 | 説明                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **顧客 id** | string   | 〇      | 顧客を識別する GUID 形式の顧客 id。             |
| **カート-id**     | string   | 〇      | カートを識別する GUID 形式のカート id。                     |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

次の表では、要求本文に含まれる[カート](cart-resources.md)のプロパティについて説明します。

| プロパティ              | 種類             | 必須        | 説明                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | string           | X              | カートが正常に作成されたときに提供されるカート識別子。                                  |
| 前のタイムスタンプ     | DateTime         | X              | カートが作成された日付 (日付/時刻形式)。 カートが正常に作成されたときに適用されます。        |
| lastModifiedTimeStamp | DateTime         | X              | カートが最後に更新された日付 (日付/時刻形式)。 カートが正常に作成されたときに適用されます。    |
| expirationTimeStamp   | DateTime         | X              | カートの有効期限が切れる日付 (日付と時刻の形式)。  カートの作成が成功したときに適用されます。            |
| lastModifiedUser      | string           | X              | カートを最後に更新したユーザー。 カートの作成が成功したときに適用されます。                             |
| lineItems             | オブジェクトの配列 | 〇             | [CartLineItem](cart-resources.md#cartlineitem)リソースの配列。                                               |


次の表では、要求本文の[CartLineItem](cart-resources.md#cartlineitem)プロパティについて説明します。

| プロパティ             | 種類                        | 必須     | 説明                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | string                      | X           | カートの品目の一意の識別子。 カートの作成が成功したときに適用されます。                |
| catalogId            | string                      | 〇          | カタログ項目の識別子。                                                                       |
| friendlyName         | string                      | X           | (省略可能)。 明確に区別できるように、パートナーによって定義された項目のフレンドリ名。              |
| quantity             | int                         | 〇          | ライセンスまたはインスタンスの数。     |
| currencyCode         | string                      | X           | 通貨コード。                                                                                 |
| 周期サイクル         | オブジェクト                      | 〇          | 現在の期間に設定されている請求サイクルの種類。                                              |
| 参加者         | オブジェクトの文字列ペアの一覧 | X           | 購入の参加者のコレクション。                                                      |
| provisioningContext  | Dictionary < string、string >  | X           | プランのプロビジョニングに使用されるコンテキスト。                                                          |
| orderGroup           | string                      | X           | 一緒に配置できる項目を示すグループ。                                            |
| error (エラー)                | オブジェクト                      | X           | エラーが発生した場合にカートが作成された後に適用されます。                                                 |


**要求の例**

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

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>REST 応答


成功した場合、このメソッドは、応答本文で設定された[カート](cart-resources.md)リソースを返します。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

**応答の例**

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

 

 




