---
title: 顧客ユーザーをロールから削除する
description: 顧客アカウント内のディレクトリロールからユーザーを削除する方法。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8bb79a0b1b1c8ef7200e02f29483014326422cb3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094894"
---
# <a name="remove-a-customer-user-from-a-role"></a>顧客ユーザーをロールから削除する

**適用対象**

- パートナー センター

顧客アカウント内のディレクトリロールからユーザーを削除する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="c"></a>C\#

ディレクトリロールからユーザーを削除するには、Iaggregatepartner.customers メソッドの呼び出しを使用してユーザーを変更する顧客を選択し、そこから[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを使用してロールを指定します。ディレクトリロール ID を指定して、 [**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid)メソッドを使用してロールを指定します。 次に、 [**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid)メソッドにアクセスして削除するユーザーを識別し、 [**Delete**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete)メソッドを使用してユーザーをロールから削除します。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: RemoveCustomerUserMemberFromDirectoryRole.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法     | 要求 URI                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **DELETE** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers/{user-ID} HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次の URI パラメーターを使用して、正しい顧客、ロール、およびユーザーを識別します。

| 名前                   | Type     | 必須 | 説明                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | この値は、顧客を識別する GUID 形式の**顧客テナント id**です。 |
| **ロール id**            | **guid** | Y        | 値は、ロールを識別する GUID 形式の**ロール id**です。                |
| **ユーザー id**            | **guid** | Y        | 値は、単一のユーザーアカウントを識別する GUID 形式の**ユーザー id**です。   |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20/directoryroles/729827e3-9c14-49f7-bb1b-9608f156bbb8/usermembers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0a00ec08-6273-46bb-ab6f-14a13959b381
MS-CorrelationId: 87d18a45-81fc-40cf-921a-b91cb82d67fe
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 応答

ユーザーがロールから正常に削除された場合、応答本文は空になります。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
