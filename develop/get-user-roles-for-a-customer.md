---
title: 顧客のユーザー ロールを取得する
description: ユーザーアカウントにアタッチされているすべてのロール/アクセス許可の一覧を取得します。 バリエーションには、顧客のすべてのユーザーアカウントのすべてのアクセス許可の一覧を取得し、特定のロールを持つユーザーの一覧を取得することが含まれます。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dad5c035c08905c3d39052de07ebb912452a16b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095195"
---
# <a name="get-user-roles-for-a-customer"></a>顧客のユーザー ロールを取得する

**適用対象**

- パートナー センター

ユーザーアカウントにアタッチされているすべてのロール/アクセス許可の一覧を取得します。 バリエーションには、顧客のすべてのユーザーアカウントのすべてのアクセス許可の一覧を取得し、特定のロールを持つユーザーの一覧を取得することが含まれます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="c"></a>C\#

指定された顧客のすべてのディレクトリロールを取得するには、最初に指定された顧客 ID を取得します。 次に、 **iaggregatepartner.customers**コレクションを使用して、 **ById ()** メソッドを呼び出します。 次に、 **Directoryroles**プロパティを呼び出し、その後に**Get ()** または**GetAsync ()** メソッドを呼び出します。

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: GetCustomerDirectoryRoles.cs

特定のロールを持つ顧客ユーザーの一覧を取得するには、まず、指定された顧客 ID とディレクトリロール ID を取得します。 次に、 **iaggregatepartner.customers**コレクションを使用して、 **ById ()** メソッドを呼び出します。 次に、 **Directoryroles**プロパティ、 **ById ()** メソッド、 **usermembers**プロパティ、およびその後に**Get ()** または**GetAsync ()** メソッドを呼び出します。

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: partnersdk. FeatureSamples**クラス**: GetCustomerDirectoryRoleUserMembers.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1 |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1                 |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers    |

### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを使用して、正しい顧客を特定します。

| 名前                   | Type     | 必須 | 説明                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | この値は、リセラーがリセラーに属する特定の顧客の結果をフィルター処理できるようにする GUID 形式の**顧客テナント id**です。                                                      |
| **ユーザー id**            | **guid** | N        | 値は、1つのユーザーアカウントに属する GUID 形式の**ユーザー id**です。                                                                                                                            |
| **ロール id**            | **guid** | N        | 値は、ロールの種類に属する GUID 形式の**ロール id**です。 すべてのユーザー アカウントを対象に、ある顧客のすべてのディレクトリ ロールを問い合わせることで、これらの ID を取得できます。 (上記の2番目のシナリオ)。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは、指定されたユーザーアカウントに関連付けられているロールの一覧を返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
      "totalCount": 2,
      "items": [
        {
          "name": "Helpdesk Administrator",
          "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
          "attributes": { "objectType": "DirectoryRole" }
        },
        {
          "name": "User Account Administrator",
          "id": "fe930be7-5e62-47db-91af-98c3a49a38b1",
          "attributes": { "objectType": "DirectoryRole" }
        }
      ],
      "attributes": { "objectType": "Collection" }
}
```
