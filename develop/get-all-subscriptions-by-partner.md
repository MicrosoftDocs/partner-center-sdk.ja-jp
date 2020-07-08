---
title: パートナー MPN ID ごとに顧客のサブスクリプションを取得する
description: 特定のパートナーから提供されたサブスクリプションの一覧を指定された顧客に取得する方法。
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 545eb08e54a5a74fb6e8ca27fd1f02d4ba5bf055
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86093903"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a>パートナー MPN ID ごとに顧客のサブスクリプションを取得する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

特定のパートナーから提供されたサブスクリプションの一覧を指定された顧客に取得する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- パートナー Microsoft Partner Network (MPN) 識別子。

## <a name="c"></a>C\#

指定された顧客に対して特定のパートナーによって提供されたサブスクリプションの一覧を取得するには、最初に顧客 ID と共に[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを使用して顧客を識別します。 次に、[**サブスクリプション**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)プロパティから顧客サブスクリプションコレクション操作へのインターフェイスを取得し、MPN ID を指定して[**ByPartner**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner)メソッドを呼び出してパートナーを識別し、パートナーサブスクリプション操作へのインターフェイスを取得します。 最後に、 [**get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get)または[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync)メソッドを呼び出して、コレクションを取得します。

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: GetSubscriptionsByMpnid.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

指定された顧客に対して特定のパートナーによって提供されたサブスクリプションの一覧を取得するには、まず、顧客 ID と共に**iaggregatepartner.customers**関数を使用して顧客を識別します。 次に、 **getsubscriptions**関数から顧客サブスクリプションコレクション操作へのインターフェイスを取得し、MPN ID を指定して**byPartner**関数を呼び出し、パートナーを識別し、パートナーサブスクリプション操作へのインターフェイスを取得します。 最後に、 **get**関数を呼び出して、コレクションを取得します。

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

指定された顧客に対して特定のパートナーから提供されたサブスクリプションの一覧を取得するには、 [**Get Partnercustomer subscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md)コマンドを実行します。 **CustomerId**パラメーターを使用して顧客を識別するための顧客 ID を指定し、 **MPNID**パラメーターに MPN ID を設定して、パートナーを識別します。

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI |
|---------|----------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions? mpn \_ id = {mpn} HTTP/1.1 |

### <a name="uri-parameters"></a>URI パラメーター

次のパスとクエリパラメーターを使用して、顧客とパートナーを識別します。

| 名前        | Type   | 必須 | 説明                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| customer-id | string | はい      | 顧客を識別する GUID 形式の文字列。       |
| mpn-id      | INT    | はい      | パートナーを識別する Microsoft Partner Network ID。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions?mpn_id=4847383 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[サブスクリプション](subscription-resources.md)リソースのコレクションが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 985
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: LdFhumtx6Ea0Kl5Z.0
MS-ServerId: 101112202
Date: Thu, 13 Apr 2017 20:58:08 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "offerName": "Intune Device",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "unitType": "Licenses",
            "creationDate": "2017-04-10T23:02:26.02Z",
            "effectiveStartDate": "2017-04-10T00:00:00Z",
            "commitmentEndDate": "2018-05-07T00:00:00Z",
            "status": "active",
            "autoRenewEnabled": true,
            "isTrial": false,
            "billingType": "license",
            "billingCycle": "monthly",
            "partnerId": "4847383",
            "contractType": "subscription",
            "links": {
                "offer": {
                    "uri": "/offers/DB2E705F-B82A-4024-A3D5-D88E12F2DB35?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            },
            "orderId": "3EDDCAC6-63B2-4C40-B0B6-F47E18301492",
            "attributes": {
                "etag": "eyJpZCI6IjQyMjI2ZWQ2LTA3MGEtNGUwZi1iODBjLTRjZGZiM2U5N2FhNyIsInZlcnNpb24iOjF9",
                "objectType": "Subscription"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="see-also"></a>関連項目

- [パートナー センターの分析 - リソース](partner-center-analytics-resources.md)
