---
title: 顧客の削除されたユーザーを表示する
description: 顧客 ID によって顧客の削除されたユーザーリソースの一覧を取得します。 必要に応じてページサイズを設定することもできます。 フィルターを指定する必要があります。
ms.assetid: B2248C7D-0F68-4F52-9249-D3168C2F6E83
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cab6b1cd309757f0754610eca362bcf205d199fb
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414253"
---
# <a name="view-deleted-users-for-a-customer"></a>顧客の削除されたユーザーを表示する


**適用対象**

- Partner Center

顧客 ID によって顧客の削除されたユーザーリソースの一覧を取得します。 必要に応じてページサイズを設定することもできます。 フィルターを指定する必要があります。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。
- 顧客識別子。

## <a name="span-idwhat_happens_when_you_delete_a_user_account_span-idwhat_happens_when_you_delete_a_user_account_span-idwhat_happens_when_you_delete_a_user_account_what-happens-when-you-delete-a-user-account"></a>ユーザーアカウントを削除するとどうなるか <span id="WHAT_HAPPENS_WHEN_YOU_DELETE_A_USER_ACCOUNT_"/><span id="what_happens_when_you_delete_a_user_account_"/><span id="What_happens_when_you_delete_a_user_account_"/>ますか?


ユーザーアカウントを削除すると、ユーザーの状態が "非アクティブ" に設定されます。 30日間はそのままで、ユーザーアカウントとそれに関連付けられたデータが消去され、回復できなくなります。 30日の期間内に削除されたユーザーアカウントを復元する場合は、「[顧客に対して削除されたユーザーを復元](restore-a-user-for-a-customer.md)する」を参照してください。 削除され、"inactive" とマークされた場合、ユーザーアカウントはユーザーコレクションのメンバーとして返されなくなります (たとえば、[[顧客のすべてのユーザーアカウントの一覧を取得](get-a-list-of-all-user-accounts-for-a-customer.md)する] を使用します)。 削除されていないユーザーの一覧を取得するには、非アクティブに設定されているユーザーアカウントを照会する必要があります。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


削除されたユーザーの一覧を取得するには、状態が非アクティブに設定されている顧客のユーザーをフィルター処理するクエリを作成します。 まず、次のコードスニペットに示すように、パラメーターを使用して[**Simplefieldfilter**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter)オブジェクトをインスタンス化することで、フィルターを作成します。 次に、 [**Buildindexedquery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery)メソッドを使用してクエリを作成します。 ページングされた結果が不要な場合は、代わりに[**Buildsimplequery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery)メソッドを使用できます。 次に、顧客 ID と共に[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを使用して顧客を識別します。 最後に、[**クエリ**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query)メソッドを呼び出して要求を送信します。

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

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: GetCustomerInactiveUsers.cs

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求


**要求の構文**

| メソッド  | 要求 URI                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/users? size = {size} & フィルター = {FILTER} HTTP/1.1 |

 

**URI パラメーター**

要求の作成時には、次のパスとクエリパラメーターを使用します。

| Name        | 種類   | 必須 | 説明                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 顧客 id | guid   | はい      | 値は、顧客を識別する GUID 形式の顧客 id です。                                                                                                            |
| size        | int    | いいえ       | 一度に表示される結果の数。 このパラメーターはオプションです。                                                                                                     |
| フィルター      | フィルター | はい      | ユーザー検索をフィルター処理するクエリ。 削除されたユーザーを取得するには、次の文字列を含めてエンコードする必要があります: {"Field": "UserState", "Value": "Inactive", "Operator": "equals"}。 |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

[なし]。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> REST 応答


成功した場合、このメソッドは、応答本文内の[ユーザー](user-resources.md#customeruser)リソースのコレクションを返します。

**応答成功およびエラーコード**

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

**応答の例**

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

 

 




