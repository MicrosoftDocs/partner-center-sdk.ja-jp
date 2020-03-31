---
title: 顧客の削除されたユーザーを復元する
description: 顧客 ID とユーザー ID を使って削除されたユーザーを復元する方法。
ms.assetid: A48A4718-6EAF-4FC8-8B44-F3FDCA2B3298
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cfedefd5b9b8547b79b817c06f44e9b21f12d51c
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415397"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>顧客の削除されたユーザーを復元する


**適用対象**

- Partner Center

顧客 ID とユーザー ID を使って削除された**ユーザー**を復元する方法。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。
- 顧客 ID (顧客-テナント id)。 顧客の ID を持っていない場合は、[顧客] リストから顧客を選択し、[アカウント] を選択して、Microsoft ID を保存することで、パートナーセンターで ID を検索できます。
- ユーザー ID。 ユーザー ID を持っていない場合は、「[顧客の削除されたユーザーの表示](view-a-deleted-user.md)」を参照してください。

## <a name="span-idwhen_can_you_restore_a_deleted_user_account_span-idwhen_can_you_restore_a_deleted_user_account_span-idwhen_can_you_restore_a_deleted_user_account_when-can-you-restore-a-deleted-user-account"></a>削除されたユーザーアカウントを復元できるのは、<span id="When_can_you_restore_a_deleted_user_account_"/><span id="when_can_you_restore_a_deleted_user_account_"/><span id="WHEN_CAN_YOU_RESTORE_A_DELETED_USER_ACCOUNT_"/>。


ユーザーアカウントを削除すると、ユーザーの状態が "非アクティブ" に設定されます。 30日間はそのままで、ユーザーアカウントとそれに関連付けられたデータが消去され、回復できなくなります。 削除されたユーザーアカウントは、この30日間の期間中のみ復元できます。 削除され、"inactive" とマークされた場合、ユーザーアカウントはユーザーコレクションのメンバーとして返されなくなります (たとえば、[[顧客のすべてのユーザーアカウントの一覧を取得](get-a-list-of-all-user-accounts-for-a-customer.md)する] を使用します)。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


ユーザーを復元するには、[**顧客ユーザー**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.customeruser)クラスの新しいインスタンスを作成し、[**ユーザーの状態**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.user.state)プロパティの値を[**UserState. Active**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.userstate)に設定します。 削除されたユーザーを復元するには、ユーザーの状態を [アクティブ] に設定します。 ユーザーリソースの残りのフィールドを再作成する必要はないことに注意してください。 これらの値は、削除済みの非アクティブなユーザーリソースから自動的に復元されます。 次に、顧客 ID と共に[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを使用して顧客を識別し、 [**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)メソッドを使用してユーザーを識別します。 最後に、 [**Patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch)メソッドを呼び出して、ユーザーを復元する要求を送信するための**ユーザー**インスタンスを渡します。

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

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: CustomerUserRestore.cs

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求


**要求の構文**

| メソッド    | 要求 URI                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **KB830347** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1 |

 

**URI パラメーター**

次のクエリパラメーターを使用して、顧客 id とユーザー id を指定します。

| Name                   | 種類     | 必須 | 説明                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **顧客-テナント id** | **guid** | Y        | この値は、リセラーが特定の顧客に対して結果をフィルター処理できるようにする GUID 形式の**顧客テナント id**です。 |
| **ユーザー id**            | **guid** | Y        | 値は、1つのユーザーアカウントに属する GUID 形式の**ユーザー id**です。                                         |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

次の表では、要求本文に必要なプロパティについて説明します。

| Name       | 種類   | 必須 | 説明                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| 状態      | string | Y        | ユーザー状態。 削除されたユーザーを復元するには、これに "active" が含まれている必要があります。 |
| 属性 | object | N        | "ObjectType": "顧客ユーザー" が含まれています。                                 |

 

**要求の例**

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

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST 応答


成功した場合、このメソッドは、復元されたユーザー情報を応答本文に返します。

**応答成功およびエラーコード**

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

**応答の例**

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
