---
title: 顧客の削除されたユーザーを復元する
description: How to restore a deleted User by customer ID and user ID.
ms.assetid: A48A4718-6EAF-4FC8-8B44-F3FDCA2B3298
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 95e74d1f7719efae7b04aba5dab3e1ad66dfa8ee
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486572"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>顧客の削除されたユーザーを復元する


**Applies To**

- パートナー センター

How to restore a deleted **User** by customer ID and user ID.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
- A customer ID (customer-tenant-id). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.
- The user ID. If you do not have the user ID, see [View deleted users for a customer](view-a-deleted-user.md).

## <a name="span-idwhen_can_you_restore_a_deleted_user_account_span-idwhen_can_you_restore_a_deleted_user_account_span-idwhen_can_you_restore_a_deleted_user_account_when-can-you-restore-a-deleted-user-account"></a><span id="When_can_you_restore_a_deleted_user_account_"/><span id="when_can_you_restore_a_deleted_user_account_"/><span id="WHEN_CAN_YOU_RESTORE_A_DELETED_USER_ACCOUNT_"/>When can you restore a deleted user account?


The user state is set to "inactive" when you delete a user account. It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable. You can only restore a deleted user account during this thirty day window. Note that once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


To restore a user, create a new instance of the [**CustomerUser**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) class, and set the value of the [**User.State**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.user.state) property to [**UserState.Active**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.userstate). You restore a deleted user by setting the user's state to active. Note that you do not have to repopulate the remaining fields in the user resource. Those values will automatically be restored from the deleted, inactive user resource. Next, use the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user. Finally, call the [**Patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) method and pass the **CustomerUser** instance to send the request to restore the user.

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

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CustomerUserRestore.cs

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request


**Request syntax**

| メソッド    | 要求 URI                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **PATCH** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1 |

 

**URI parameter**

Use the following query parameters to specify the customer id and user id.

| 名前                   | タスクバーの検索ボックスに     | 必須かどうか | 説明                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results to a given customer. |
| **user-id**            | **guid** | Y        | The value is a GUID formatted **user-id** that belongs to a single user account.                                         |

 

**Request headers**

- See [Partner Center REST Headers](headers.md) for more information.

**Request body**

This table describes the required properties in the request body.

| 名前       | タスクバーの検索ボックスに   | 必須かどうか | 説明                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| 都道府県      | string | Y        | The user state. To restore a deleted user, this must contain "active". |
| 属性 | オブジェクト | N        | Contains "ObjectType": "CustomerUser".                                 |

 

**Request example**

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

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST Response


If successful, this method returns the restored user information in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST Error Codes](error-codes.md).

**Response example**

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
