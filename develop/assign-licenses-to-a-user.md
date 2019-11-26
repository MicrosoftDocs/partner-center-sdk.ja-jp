---
title: ユーザーにライセンスを割り当てる
description: How to assign licenses to a customer user.
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

How to assign licenses to a customer user.

## <a name="prerequisites"></a>前提条件

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
- A customer identifier. The customer should have a subscription with an available license to assign.
- A customer user identifier. This identifies the user to whom to assign the license.
- A product SKU identifier that identifies the product for the license.

## <a name="assigning-licenses-through-code"></a>Assigning licenses through code

When you assign licenses to a user you must choose from the customer's collection of subscribed SKUs. Then, having identified the products that you want to assign, you must obtain the product SKU ID for each product in order to make the assignments. Each [**SubscribedSku**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) instance contains a [**ProductSku**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) property from which you can reference the [**ProductSku**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) object and get the [**ID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).

A license assignment request must contain licenses from a single license group. For example, you cannot assign licenses from [**Group1**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) and **Group2** in the same request. An attempt to assign licenses from more than one group in a single request will fail with an appropriate error. To find out what licenses are available by license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).

Here are the steps to assign licenses through code:

1. Instantiate a [**LicenseAssignment**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object. You use this object to specify the product SKU and service plans to assign.

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. Populate the object properties as shown below. This code assumes that you already have the product SKU ID, and that all of the available service plans will be assigned (i.e. none will be excluded).
  
    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. If you don't have the product SKU ID, you need to retrieve the collection of subscribed SKUs and get the product SKU ID from one of them. Here is an example if you know the product SKU name.

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. Next, instantiate a new list of type [**LicenseAssignment**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment), and add the license object. You can assign more than one license by adding each individually to the list. The licenses included in this list must be from the same license group.

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. Create a [**LicenseUpdate**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. Call the [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object as shown below to assign the licenses.

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

To assign a license to a customer user, first instantiate a [**LicenseAssignment**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object, and populate the [**Skuid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) and [**ExcludedPlans**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) properties. You use this object to specify the product SKU to assign and service plans to exclude. Next, instantiate a new list of type **LicenseAssignment**, and add the license object to the list. Then create a [**LicenseUpdate**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.

Next, use the [**IAggregatePartner.Customers.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user. Then get an interface to customer user license update operations from the [**LicenseUpdates**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) property.

Finally, call the [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object to assign the license.

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

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CustomerUserAssignLicenses.cs

## <a name="request"></a>要求

### <a name="request-syntax"></a>要求の構文

| メソッド   | 要求 URI                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

Use the following path parameters to identify the customer and user.

| 名前        | タスクバーの検索ボックスに   | 必須かどうか | 説明                                       |
|-------------|--------|----------|---------------------------------------------------|
| customer-id | string | [はい]      | A GUID formatted ID that identifies the customer. |
| user-id     | string | [はい]      | A GUID formatted ID that identifies the user.     |

### <a name="request-headers"></a>要求ヘッダー

See [Partner Center REST headers](headers.md) for more information.

### <a name="request-body"></a>要求本文

You must include a [LicenseUpdate](license-resources.md#licenseupdate) resource in the request body that specifies the licenses to assign.

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

## <a name="rest-response"></a>REST Response

If successful, an HTTP response status code 201 is returned and the response body contains a [LicenseUpdate](license-resources.md#licenseupdate) resource with the license information.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

### <a name="response-example-success"></a>Response example (success)

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

### <a name="response-example-license-is-not-available"></a>Response example (license is not available)

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