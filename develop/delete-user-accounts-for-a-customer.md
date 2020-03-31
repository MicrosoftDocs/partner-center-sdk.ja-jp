---
title: 顧客のユーザーアカウントを削除する
description: 顧客の既存のユーザーアカウントを削除する方法。
ms.assetid: 12097809-A62D-4929-9F1D-08676784BA39
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 728694cc236e0257a24940ad4c3a9284e4e28b21
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415589"
---
# <a name="delete-a-user-account-for-a-customer"></a>顧客のユーザーアカウントを削除する

適用対象

- Partner Center

このトピックでは、顧客の既存のユーザーアカウントを削除する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。
- 顧客 ID (**顧客-テナント id**)。 お客様の ID をお持ちでない場合は、パートナーセンターで ID を参照してください。 顧客 の一覧から顧客を選択し、**アカウント** を選択して、Microsoft ID を保存します。
- ユーザー ID。 ユーザー ID を持っていない場合は、「[顧客のすべてのユーザーアカウントの一覧を取得](get-a-list-of-all-user-accounts-for-a-customer.md)する」を参照してください。

## <a name="deleting-a-user-account"></a>ユーザー アカウントを削除する

ユーザーアカウントを削除すると、ユーザー状態は30日間**非アクティブ**に設定されます。 30日後に、ユーザーアカウントとそれに関連付けられたデータが消去され、回復できなくなります。

非アクティブなアカウントが30日の期間内にある場合は、[削除されたユーザーアカウントを顧客に対して復元](restore-a-user-for-a-customer.md)できます。 ただし、削除され、非アクティブとマークされているアカウントを復元すると、そのアカウントはユーザーコレクションのメンバーとして返されなくなります (たとえば、[顧客のすべてのユーザーアカウントの一覧を取得](get-a-list-of-all-user-accounts-for-a-customer.md)した場合)。

## <a name="c"></a>C\#

既存の顧客のユーザーアカウントを削除するには:

1. 顧客 ID を指定して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを使用し、顧客を識別します。
2. ユーザーを識別するには、 [**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)メソッドを呼び出します。
3. [**Delete**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete)メソッドを呼び出してユーザーを削除し、ユーザー状態を非アクティブに設定します。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: DeleteCustomerUser.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド     | 要求 URI                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| DELETE     | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

次のクエリパラメーターを使用して、顧客とユーザーを識別します。

| Name                   | 種類     | 必須 | 説明                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| customer-tenant-id     | GUID     | Y        | 値は GUID 形式の**顧客テナント id**で、リセラーは特定の顧客の結果をフィルター処理できます。 |
| ユーザー id                | GUID     | Y        | 値は、1つのユーザーアカウントに属する GUID 形式の**ユーザー id**です。                                          |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし]。

### <a name="request-example"></a>要求の例

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは、コンテンツステータスコード " **204 なし**" を返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
