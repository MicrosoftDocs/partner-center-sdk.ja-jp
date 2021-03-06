---
title: サブスクリプションのサポート連絡先情報を取得する
description: サブスクリプションのサポート連絡先を取得する方法。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df3bce48902d95dc541c4a45e4e633569fc4406e
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927253"
---
# <a name="get-a-subscriptions-support-contact"></a>サブスクリプションのサポート連絡先情報を取得する

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

サブスクリプションのサポート連絡先を取得する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- サブスクリプション識別子。

## <a name="c"></a>C\#

サブスクリプションのサポート連絡先を取得するには、まず、顧客 ID と共に [**ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) メソッドを使用して顧客を識別します。 次に、サブスクリプション ID を使用して [**ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) メソッドを呼び出すことにより、サブスクリプション操作へのインターフェイスを取得します。 次に、 [**supportcontact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) プロパティを使用して contact 操作をサポートするインターフェイスを取得し、 [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) または [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) メソッドを呼び出して [**supportcontact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) オブジェクトを取得します。

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve subscription's support contact.
var supportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).SupportContact.Get();
```

**サンプル**: [コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル **クラス**: GetSubscriptionSupportContact.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/supportcontact HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次のパスパラメーターを使用して、顧客とサブスクリプションを識別します。

| 名前            | 種類   | 必須 | 説明                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| customer-id     | string | はい      | 顧客を識別する GUID 形式の文字列。           |
| subscription-id | string | はい      | 評価版サブスクリプションを識別する GUID 形式の文字列。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には [Supportcontact](subscription-resources.md#supportcontact) リソースが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「 [パートナーセンターのエラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a6c552a8-1922-4d0c-bb94-335a33334d14
MS-RequestId: d052776c-e8fd-4803-b6a3-1659055ac3c4
MS-CV: bLbUhqy0+ESOX1v4.0
MS-ServerId: 201022015
Date: Tue, 20 Jun 2017 19:30:19 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
