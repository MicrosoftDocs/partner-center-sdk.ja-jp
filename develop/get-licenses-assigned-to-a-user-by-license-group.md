---
title: ユーザーに割り当てられたライセンスをライセンス グループ別に取得する
description: 指定されたライセンスグループに割り当てられたユーザーライセンスの一覧を取得する方法。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b4997be87b31c9b86e7e214326485108a07d0797
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096805"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a>ユーザーに割り当てられたライセンスをライセンス グループ別に取得する

**適用対象**

- パートナー センター

指定されたライセンスグループに割り当てられたユーザーライセンスの一覧を取得する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- ユーザー識別子。

- 1つまたは複数のライセンスグループ識別子の一覧。

## <a name="c"></a>C\#

指定したライセンスグループからユーザーに割り当てられているライセンスを確認するには、まず「 [**Licensegroupid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)」という種類の[リスト](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1)をインスタンス化してから、一覧にライセンスグループを追加します。 次に、顧客 ID と共に[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを使用して顧客を識別します。 次に、ユーザー ID を指定して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)メソッドを呼び出し、ユーザーを識別します。 次に、[[**ライセンス**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses)] プロパティから顧客のユーザーライセンス操作へのインターフェイスを取得します。 最後に、ライセンスグループの一覧を[**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get)または[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync)メソッドに渡して、ユーザーに割り当てられているライセンスのコレクションを取得します。

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get the group1 (Azure Active Directory (AAD)) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1 };
var customerUserAadAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get the group2 (Minecraft) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group2 };
var customerUserSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get both AAD and Minecraft assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1, LicenseGroupId.Group2 };
var customerUserBothAadAndSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/V1/customers/{customer-id}/users/{user-id}/licenses? licenseGroupIds = Group1 HTTP/1.1                        |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/V1/customers/{customer-id}/users/{user-id}/licenses? licenseGroupIds = Group2 HTTP/1.1                        |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/V1/customers/{customer-id}/users/{user-id}/licenses? Licensegroupids = Group1&Licensegroupids = Group2 HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次のパスとクエリパラメーターを使用して、顧客、ユーザー、およびライセンスグループを識別します。

| 名前            | Type   | 必須 | 説明                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| customer-id     | string | はい      | 顧客を識別する GUID 形式の文字列。                                                                                                                                                                                                                 |
| user-id         | string | はい      | ユーザーを識別する GUID 形式の文字列。                                                                                                                                                                                                                     |
| licenseGroupIds | 文字列 | いいえ       | 割り当てられたライセンスのライセンスグループを示す列挙値。 有効な値: Group1、Group2 Group1-このグループには、Azure Active Directory (AAD) で管理できるライセンスを持つすべての製品が含まれています。 Group2-このグループには、Minecraft 製品ライセンスのみが含まれています。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[ライセンス](license-resources.md#license)リソースのコレクションが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
    "totalCount": 2,
    "items": [{
            "servicePlans": [

            ],
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "licenseGroupId": "group2"
            },
            "attributes": {
                "objectType": "License"
            }
        }, {
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
                "licenseGroupId": "group1"
            },
            "attributes": {
                "objectType": "License"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-no-matching-licenses-found"></a>応答の例 (一致するライセンスが見つかりません)

指定したライセンスグループに一致するライセンスが見つからない場合、応答には、値が0の totalCount 要素を持つ空のコレクションが含まれます。

```http
HTTP/1.1 200 OK
Content-Length: 71
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: q05xrhUeDUKvhrFt.0
MS-ServerId: 030020525
Date: Fri, 09 Jun 2017 22:50:11 GMT

{
    "totalCount": 0,
    "items": [],
    "attributes": {
        "objectType": "Collection"
    }
}
```
