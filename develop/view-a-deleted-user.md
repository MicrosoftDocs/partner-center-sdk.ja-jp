---
title: 顧客の削除されたユーザーを表示する
description: 顧客 ID によって顧客の削除されたユーザーリソースの一覧を取得します。 必要に応じてページサイズを設定することもできます。 フィルターを指定する必要があります。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dd7b573cca5810195d840fcb729850f981e55a51
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925540"
---
# <a name="view-deleted-users-for-a-customer"></a>顧客の削除されたユーザーを表示する

**適用対象**

- パートナー センター

顧客 ID によって顧客の削除されたユーザーリソースの一覧を取得します。 必要に応じてページサイズを設定することもできます。 フィルターを指定する必要があります。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="what-happens-when-you-delete-a-user-account"></a>ユーザーアカウントを削除するとどうなりますか。

ユーザーアカウントを削除すると、ユーザーの状態が "非アクティブ" に設定されます。 30日間はそのままで、ユーザーアカウントとそれに関連付けられたデータが消去され、回復できなくなります。 30日の期間内に削除されたユーザーアカウントを復元する場合は、「 [顧客に対して削除されたユーザーを復元](restore-a-user-for-a-customer.md)する」を参照してください。 削除され、"inactive" とマークされた場合、ユーザーアカウントはユーザーコレクションのメンバーとして返されなくなります (たとえば、[ [顧客のすべてのユーザーアカウントの一覧を取得](get-a-list-of-all-user-accounts-for-a-customer.md)する] を使用します)。 削除されていないユーザーの一覧を取得するには、非アクティブに設定されているユーザーアカウントを照会する必要があります。

## <a name="c"></a>C\#

削除されたユーザーの一覧を取得するには、状態が非アクティブに設定されている顧客のユーザーをフィルター処理するクエリを作成します。 まず、次のコードスニペットに示すように、パラメーターを使用して [**Simplefieldfilter**/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) オブジェクトをインスタンス化することによって、フィルターを作成します。 次に、[**Buildindexedquery**/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) メソッドを使用してクエリを作成します。 ページングされた結果が不要な場合は、代わりに [**Buildsimplequery**/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery] メソッドを使用できます。 次に、顧客 ID と共に [**iaggregatepartner.customers. ById**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) メソッドを使用して顧客を識別します。 最後に、[**Query**/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) メソッドを呼び出して要求を送信します。

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

**サンプル**: [コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル **クラス**: GetCustomerInactiveUsers.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users? size = {size} &フィルター = {FILTER} HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

要求の作成時には、次のパスとクエリパラメーターを使用します。

| 名前        | 種類   | 必須 | 説明                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| customer-id | guid   | Yes      | 値は、顧客を識別する GUID 形式の顧客 id です。                                                                                                            |
| サイズ        | INT    | いいえ       | 一度に表示される結果の数。 このパラメーターは省略できます。                                                                                                     |
| filter      | filter | Yes      | ユーザーの検索をフィルター処理するクエリ。 削除されたユーザーを取得するには、文字列 {"Field":"UserState","Value":"Inactive","Operator":"equals"} を含めてエンコードする必要があります。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは、応答本文内の [ユーザー](user-resources.md#customeruser) リソースのコレクションを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
