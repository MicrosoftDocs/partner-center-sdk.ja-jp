---
title: 顧客のユーザー アカウントを作成する
description: 顧客の新しいユーザーアカウントを作成します。
ms.date: 05/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 9131a1c4c37d07b1994b67379ec8361fda13a371
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094360"
---
# <a name="create-user-accounts-for-a-customer"></a>顧客のユーザー アカウントを作成する

**適用対象:**

- パートナー センター

顧客の新しいユーザーアカウントを作成します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="c"></a>C\#

顧客の新しいユーザーアカウントを取得するには、次のようにします。

1. 関連するユーザー情報を使用して、新しい **CustomerUser** オブジェクトを作成します。

2. **IAggregatePartner.Customers** コレクションを使用し、**ById()** メソッドを呼び出します。

3. **Users** プロパティを呼び出した後、**Create** メソッドを呼び出します。

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// var SelectedCustomer;

var userToCreate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "Password!1" },
    DisplayName = "TestDisplayName",
    FirstName = "TestFirstName",
    LastName = "TestLastName",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

User createdUser = partnerOperations.Customers.ById(selectedCustomerId).Users.Create(userToCreate);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: partnersdk. FeatureSamples**クラス**: CustomerUserCreate.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法   | 要求 URI                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

次のクエリ パラメーターを使用し、正しい顧客を特定します。

| 名前 | Type | 必須 | 説明 |
|----- |----- | -------- |------------ |
| **customer-tenant-id** | **guid** | Y | 値は、GUID 形式の**顧客テナント id**です。これにより、リセラーは、リセラーに属する特定の顧客の結果をフィルター処理できます。 |
| **ユーザー id** | **guid** | N | 値は、1つのユーザーアカウントに属する GUID 形式の**ユーザー id**です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "country/region code",
      "userPrincipalName": "userid@domain.onmicrosoft.com",
      "firstName": "First",
      "lastName": "Last",
      "displayName": "User name",
      "immutableId": "Some unique ID",
      "passwordProfile":{
                 password: "abCD123*",
                 forceChangePassword: true
      },
      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは GUID を含むユーザーアカウントを返します。

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
  "usageLocation": "country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "userid@domain.onmicrosoft.com",
  "firstName": "First",
  "lastName": "Last",
  "displayName": "User name",
  "immutableId": "Some unique ID",
  "passwordProfile": {
    "forceChangePassword": true,
    "password": "abCD123*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```