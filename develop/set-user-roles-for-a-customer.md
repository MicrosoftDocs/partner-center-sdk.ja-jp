---
title: 顧客のユーザー ロールを設定する
description: 顧客アカウント内には、一連のディレクトリロールがあります。 これらのロールにユーザーアカウントを割り当てることができます。
ms.assetid: B7FA3599-9AE9-4494-90B4-F7C9A2EF2338
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: edc706d791b12268cbd39ba356bee9199bdeaa54
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415225"
---
# <a name="set-user-roles-for-a-customer"></a>顧客のユーザー ロールを設定する


**適用対象**

- Partner Center

顧客アカウント内には、一連のディレクトリロールがあります。 これらのロールにユーザーアカウントを割り当てることができます。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。
- 顧客 ID (顧客-テナント id)。 顧客の ID を持っていない場合は、[顧客] リストから顧客を選択し、[アカウント] を選択して、Microsoft ID を保存することで、パートナーセンターで ID を検索できます。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


顧客ユーザーにディレクトリロールを割り当てるには、関連するユーザーの詳細を使用して新しい[**Usermember**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.roles.usermember)を作成します。 次に、指定した顧客 ID を使用して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出し、顧客を識別します。 そこから、ディレクトリロール ID と共に[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid)メソッドを使用してロールを指定します。 次に、 **Usermembers**コレクションにアクセスし、 [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create)メソッドを使用して、そのロールに割り当てられたユーザーメンバーのコレクションに新しいユーザーメンバーを追加します。

``` csharp
// UserMember createdUser;
// IAggregatePartner partnerOperations;
// Customer selectedCustomer;
// IDirectoryRole selectedRole;

// Create the new user member.
UserMember userMemberToAdd = new UserMember()
{
    UserPrincipalName = createdUser.UserPrincipalName,
    DisplayName = createdUser.DisplayName,
    Id = createdUser.Id
};

// Add the new user member to the role.
var userMemberAdded = partnerOperations.Customers.ById(selectedCustomer.Id).DirectoryRoles.ById(selectedRole.Id).UserMembers.Create(userMemberToAdd);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: AddUserMemberToDirectoryRole.cs

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求


**要求の構文**

| メソッド   | 要求 URI                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1 |

 

**URI パラメーター**

次の URI パラメーターを使用して、適切な顧客とロールを識別します。 ロールを割り当てるユーザーを識別するには、要求本文に識別情報を指定します。

| Name                   | 種類     | 必須 | 説明                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **顧客-テナント id** | **guid** | Y        | この値は、リセラーがリセラーに属する特定の顧客の結果をフィルター処理できるようにする GUID 形式の**顧客テナント id**です。 |
| **ロール id**            | **guid** | Y        | 値は、ユーザーに割り当てるロールを識別する GUID 形式の**ロール id**です。                                                              |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

次の表では、要求本文に必要なプロパティについて説明します。

| Name                  | 種類       | 必須 | 説明                            |
|-----------------------|------------|----------|----------------------------------------|
| **番号**                | **文字列** | Y        | ロールに追加するユーザーの Id。 |
| **DisplayName**       | **文字列** | Y        | ユーザーの表示名。 |
| **UserPrincipalName** | **文字列** | Y        | ユーザープリンシパルの名前。        |
| **アトリビュート**        | **素材** | Y        | "ObjectType": "UserMember" が含まれています。     |

 

**要求の例**

```http
POST https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/directoryroles/f023fd81-a637-4b56-95fd-791ac0226033/usermembers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 180
Expect: 100-continue

{
    "Id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "DisplayName": "Daniel Tsai",
    "UserPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "Attributes": {
        "ObjectType": "UserMember"
    }
}
```

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST 応答


このメソッドは、ユーザーにロールが割り当てられたときに、ロール id が割り当てられたユーザーアカウントを返します。

**応答成功およびエラーコード**

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

**応答の例**

```http
HTTP/1.1 201 Created
Content-Length: 231
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CV: aia94+gnrEeQqkGr.0
MS-ServerId: 101112202
Date: Tue, 20 Dec 2016 23:36:55 GMT

{
    "displayName": "Daniel Tsai",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "roleId": "f023fd81-a637-4b56-95fd-791ac0226033",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "attributes": {
        "objectType": "UserMember"
    }
}
```

 

 




