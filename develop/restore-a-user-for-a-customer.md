---
title: 顧客の削除されたユーザーを復元する
description: 顧客 ID とユーザー ID を使って削除されたユーザーを復元する方法。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2d46983b487817fc7152420af1b9332b53dba77b
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926475"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>顧客の削除されたユーザーを復元する

**適用対象**

- パートナー センター

顧客 ID とユーザー ID を使って削除された **ユーザー** を復元する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- ユーザー ID。 ユーザー ID を持っていない場合は、「 [顧客の削除されたユーザーの表示](view-a-deleted-user.md)」を参照してください。

## <a name="when-can-you-restore-a-deleted-user-account"></a>削除されたユーザーアカウントを復元できるのはいつですか。

ユーザーアカウントを削除すると、ユーザーの状態が "非アクティブ" に設定されます。 30日間はそのままで、ユーザーアカウントとそれに関連付けられたデータが消去され、回復できなくなります。 削除されたユーザーアカウントは、この30日の期間中のみ復元できます。 削除され、"inactive" とマークされると、ユーザーアカウントはユーザーコレクションのメンバーとして返されなくなります (たとえば、[ [顧客のすべてのユーザーアカウントの一覧を取得する](get-a-list-of-all-user-accounts-for-a-customer.md)] を使用します)。

## <a name="c"></a>C\#

ユーザーを復元するには、[**顧客ユーザー**/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) クラスの新しいインスタンスを作成し、**[/dotnet/api/microsoft.store.partnercenter.models.users.user.state]** プロパティの値を [**UserState. Active**/dotnet/api/microsoft.store.partnercenter.models.users.userstate] に設定します。

削除されたユーザーを復元するには、ユーザーの状態を [アクティブ] に設定します。 ユーザーリソースの残りのフィールドを再設定する必要はありません。 これらの値は、削除済みの非アクティブなユーザーリソースから自動的に復元されます。 次に、顧客 ID と共に [**iaggregatepartner.customers. ById**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) メソッドを使用して顧客を識別し、[**ById**/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) メソッドを使用してユーザーを識別します。

最後に、[**Patch**/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) メソッドを呼び出して、ユーザーを復元するための要求を送信するように **顧客ユーザー** インスタンスを渡します。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

**サンプル**: [コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル **クラス**: CustomerUserRestore.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法    | 要求 URI                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを使用して、顧客 id とユーザー id を指定します。

| 名前                   | 種類     | 必須 | 説明                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | この値は、リセラーが特定の顧客に対して結果をフィルター処理できるようにする GUID 形式の **顧客テナント id** です。 |
| **ユーザー id**            | **guid** | Y        | 値は、1つのユーザーアカウントに属する GUID 形式の **ユーザー id** です。                                         |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

次の表では、要求本文に必要なプロパティについて説明します。

| 名前       | 種類   | 必須 | 説明                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| State      | string | Y        | ユーザーの状態。 削除されたユーザーを復元するには、この文字列に "active" が含まれている必要があります。 |
| 属性 | object | N        | "ObjectType": "顧客ユーザー" が含まれています。                                 |

### <a name="request-example"></a>要求の例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答は応答本文で復元されたユーザー情報を返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「 [パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
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
```
