---
title: 注文明細項目によるアクティブ化リンクの取得
description: 注文明細項目によってサブスクリプションのアクティブ化リンクを取得します。
ms.assetid: ff1c1b59-f6c2-4f17-b0d6-00109761a1fd
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: fc455a11c854b6998b23c0810d26f364eb50e6e9
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486072"
---
# <a name="get-activation-link-by-order-line-item"></a>注文明細項目によるアクティブ化リンクの取得

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

注文明細項目番号によって、コマーシャル marketplace のサブスクリプションアクティブ化リンクを取得します。

パートナーセンターのダッシュボードでは、メインページで [サブスクリプション] の下にある**特定**の**サブスクリプション**を選択するか、 **[サブスクリプション] ページで**アクティブにするサブスクリプションの横にある **[パブリッシャーのサイトへのジャンプ]** リンクを選択することで、この操作を実行できます。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- アクティブ化が必要な製品の完了した注文。

## <a name="span-idexamplesspan-idexamplesspan-idexamplesexamples"></a><span id="Examples"/><span id="examples"><span id="EXAMPLES"/>の例

### <a name="c"></a>C#

行項目のアクティベーションリンクを取得するには、 [**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers)コレクションを使用し、選択した顧客 ID を使用して[**ById ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出します。 次に、 [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders)プロパティと、指定した[**OrderId**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order.id)を使用して[**ById ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)メソッドを呼び出します。 次に、行項目番号の識別子を指定して、 [**LineItems**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById ()** メソッドを呼び出します。  最後に、 **ActivationLinks ()** メソッドを呼び出します。

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item 
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求

**要求の構文**

| メソッド  | 要求 URI                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1 |

**要求ヘッダー**

詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST 応答

成功した場合、このメソッドは応答本文で[顧客](customer-resources.md#customer)リソースのコレクションを返します。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 809
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT
{
  "totalCount": 1,
  "items": [
    {
      "lineItemNumber": 0,
      "link": {
        "uri": "<link populated here>",
        "method": "GET",
        "headers": [
          
        ]
      }
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks",
      "method": "GET",
      "headers": [
        
      ]
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```
