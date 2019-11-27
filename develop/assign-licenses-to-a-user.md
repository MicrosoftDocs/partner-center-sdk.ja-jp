---
title: ユーザーにライセンスを割り当てる
description: 顧客ユーザーにライセンスを割り当てる方法。
ms.assetid: 872C7444-DF89-4EB5-8C1E-1D8E2934A40E
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 615e2dba04556647c358d5b382047e37e70606f8
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489192"
---
# <a name="assign-licenses-to-a-user"></a>ユーザーにライセンスを割り当てる

適用対象:

- パートナー センター

顧客ユーザーにライセンスを割り当てる方法。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。
- 顧客識別子。 お客様は、割り当てに使用できるライセンスを持つサブスクリプションを所有している必要があります。
- 顧客のユーザー id。 これにより、ライセンスを割り当てるユーザーが識別されます。
- ライセンスの製品を識別する製品 SKU 識別子。

## <a name="assigning-licenses-through-code"></a>コードを使用したライセンスの割り当て

ユーザーにライセンスを割り当てるときは、お客様のサブスクライブ済み Sku のコレクションから選択する必要があります。 次に、割り当てる製品を特定した後、割り当てを行うために各製品の製品 SKU ID を取得する必要があります。 各[**SubscribedSku**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku)インスタンスには[ **、productsku オブジェクトを**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku)参照して[**ID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id)を取得できる[**productsku**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku)プロパティが含まれています。

ライセンス割り当て要求には、1つのライセンスグループのライセンスが含まれている必要があります。 たとえば、同じ要求で[**Group1**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)と**Group2**からライセンスを割り当てることはできません。 1つの要求で複数のグループからライセンスを割り当てようとすると、適切なエラーが発生して失敗します。 ライセンスグループごとに利用可能なライセンスを確認するには、「[ライセンスグループ別の使用可能なライセンスの一覧を取得](get-a-list-of-available-licenses-by-license-group.md)する」を参照してください。

コードを使用してライセンスを割り当てる手順は次のとおりです。

1. [**Licenseassignment**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)オブジェクトをインスタンス化します。 このオブジェクトを使用して、割り当てる製品 SKU とサービスプランを指定します。

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. 次に示すように、オブジェクトのプロパティを設定します。 このコードでは、製品 SKU ID が既に存在し、利用可能なすべてのサービスプランが割り当てられていることを前提としています (つまり、除外されません)。
  
    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. 製品 SKU ID を持っていない場合は、サブスクライブされた Sku のコレクションを取得し、そのうちの1つから製品 SKU ID を取得する必要があります。 製品 SKU 名がわかっている場合の例を次に示します。

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. 次に、 [**Licenseassignment**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)型の新しいリストをインスタンス化し、ライセンスオブジェクトを追加します。 複数のライセンスを割り当てるには、それぞれを一覧に個別に追加します。 この一覧に含まれるライセンスは、同じライセンスグループのものである必要があります。

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. [**Licenseupdate**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate)インスタンスを作成し、ライセンスの割り当ての一覧を[**licensestoassign**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)プロパティに割り当てます。

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create)または[**createasync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync)メソッドを呼び出し、次のようにライセンスの更新オブジェクトを渡してライセンスを割り当てます。

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

顧客ユーザーにライセンスを割り当てるには、まず、 [**Licenseassignment**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)オブジェクトをインスタンス化し、 [**Skuid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid)プロパティと[**ExcludedPlans**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans)プロパティを設定します。 このオブジェクトを使用して、割り当てる製品 SKU と、除外するサービスプランを指定します。 次に、 **Licenseassignment**型の新しいリストをインスタンス化し、ライセンスオブジェクトをリストに追加します。 次に、 [**Licenseupdate**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate)インスタンスを作成し、ライセンスの割り当ての一覧を[**licensestoassign**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)プロパティに割り当てます。

次に、顧客 ID と共に[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを使用して顧客を識別し、 [**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)メソッドにユーザー id を指定してユーザーを識別します。 次に、 [**Licenseupdates**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates)プロパティから顧客のユーザーライセンスの更新操作へのインターフェイスを取得します。

最後に、 [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create)または[**createasync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync)メソッドを呼び出し、ライセンスの更新オブジェクトを渡してライセンスを割り当てます。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerUserId;
// string selectedCustomerId;
// string selectedProductSkuId;

// Instantiate and populate a LicenseAssignment object.
LicenseAssignment license = new LicenseAssignment();
license.SkuId = selectedProductSkuId;
license.ExcludedPlans = null;

// Instantiate a list of licenses to assign and add the license to it.
List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
licenseList.Add(license);

// Instantiate a LicenseUpdate object and add the list of licenses to assign.
LicenseUpdate updateLicense = new LicenseUpdate();
updateLicense.LicensesToAssign = licenseList;

// Update the user licenses.
var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: CustomerUserAssignLicenses.cs

## <a name="request"></a>要求

### <a name="request-syntax"></a>要求の構文

| メソッド   | 要求 URI                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **投稿** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

次のパスパラメーターを使用して、顧客とユーザーを識別します。

| 名前        | 種類   | 必須 | 説明                                       |
|-------------|--------|----------|---------------------------------------------------|
| 顧客 id | string | 〇      | 顧客を識別する GUID 形式の ID。 |
| ユーザー id     | string | 〇      | ユーザーを識別する GUID 形式の ID。     |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

割り当てるライセンスを指定する[Licenseupdate](license-resources.md#licenseupdate)リソースを要求本文に含める必要があります。

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/554526aa-cf5e-46fa-95df-98dbc55d8a1e/licenseupdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 183
Expect: 100-continue

{
    "LicensesToAssign": [{
            "ExcludedPlans": null,
            "SkuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "LicensesToRemove": null,
    "LicenseWarnings": null,
    "Attributes": {
        "ObjectType": "LicenseUpdate"
    }
}
```

## <a name="rest-response"></a>REST 応答

成功すると、HTTP 応答ステータスコード201が返され、応答本文にはライセンス情報を含む[Licenseupdate](license-resources.md#licenseupdate)リソースが含まれます。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

### <a name="response-example-success"></a>応答の例 (成功)

```http
HTTP/1.1 201 Created
Content-Length: 139
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CV: 5AnzcZQrvUqCq3kd.0
MS-ServerId: 030020525
Date: Thu, 20 Apr 2017 21:50:39 GMT

{
    "licensesToAssign": [{
            "skuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "licenseWarnings": [],
    "attributes": {
        "objectType": "LicenseUpdate"
    }
}
```

### <a name="response-example-license-is-not-available"></a>応答の例 (ライセンスは使用できません)

```http
HTTP/1.1 400 Bad Request
Content-Length: 341
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: f4f3b748-8b22-4d07-a5a1-dceb32824192
MS-CV: 5npA0K22CUmWPOzB.0
MS-ServerId: 102030524
Date: Thu, 20 Apr 2017 22:12:36 GMT

{
    "code": 60012,
    "description": "We&#39;re sorry, it looks like you've run out of licenses. Buy more licenses, and then try again.",
    "data": ["LicenseQuotaExceededException : Subscription with Account 0c39d6d5-c70d-4c55-bc02-f620844f3fd1 and SKU f8a1db68-be16-40ed-86d5-cb42ce701560 does not have any available licenses left."],
    "source": "PartnerFD"
}
```