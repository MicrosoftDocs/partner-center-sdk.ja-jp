---
title: 間接リセラーの顧客を作成する
description: 間接プロバイダーは、間接リセラーの顧客を作成できます。
ms.assetid: F6196EE1-1B72-4D0A-BE6E-56A243671CDE
ms.date: 06/03/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b6f41d4e76cc41d9a2611c95762954e37157f8ab
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488772"
---
# <a name="create-a-customer-for-an-indirect-reseller"></a>間接リセラーの顧客を作成する

適用対象:

- パートナー センター

間接プロバイダーは、間接リセラーの顧客を作成できます。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。
- 間接リセラーのテナント識別子。
- 間接リセラーは、間接プロバイダとのパートナーシップを持っている必要があります。

## <a name="c"></a>C\#

間接リセラーに新しい顧客を追加するには、次のようにします。

1. 新しい[**Customer**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer)オブジェクトをインスタンス化し、そのインスタンスを作成して、その[**プロファイル**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile)と会社の[**プロファイル**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)を作成します。 必ず間接リセラー ID を[**AssociatedPartnerID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid)プロパティに割り当ててください。
2. 顧客コレクション操作へのインターフェイスを取得するには、 [**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers)プロパティを使用します。 
3. 顧客を作成するには、 [**create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create)または[**createasync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)メソッドを呼び出します。

### <a name="c-example"></a>C\# の例

``` csharp
// IAggregatePartner partnerOperations;
// var indirectResellerId;
var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "WingtipToys{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "Gena@wingtiptoys.com",
        Language = "En",
        CompanyName = "Wingtip Toys" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Gena",
            LastName = "Soto",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = "4255550101"
        }
    },
    AssociatedPartnerId = indirectResellerId
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: CreateCustomerforIndirectReseller.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド   | 要求 URI                                                       |
|----------|-------------------------------------------------------------------|
| **投稿** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

次の表では、要求本文に必要なプロパティについて説明します。

| 名前                                          | 種類   | 必須 | 説明                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BillingProfile](#billing-profile)             | オブジェクト | 〇      | 顧客の請求プロファイル情報。                                                                                                                                                                                                                                                                                                           |
| [会社のプロファイル](#company-profile)             | オブジェクト | 〇      | 顧客の会社のプロファイル情報。                                                                                                                                                                                                                                                                                                           |
| [AssociatedPartnerId](customer-resources.md#customer) | string | 〇      | 間接リセラー ID。 ここで指定する ID によって示される間接リセラーは、間接プロバイダーとのパートナーシップを持つ必要があります。間接リセラーの場合、要求は失敗します。 また、AssociatedPartnerId 値が指定されていない場合、顧客は間接リセラーではなく間接プロバイダーの直接の顧客として作成されることに注意してください。 |

#### <a name="billing-profile"></a>課金プロファイル

次の表では、新しい顧客を作成するために必要な、ユーザーごとの[プロファイル](customer-resources.md#customerbillingprofile)リソースの最小限の必須フィールドについて説明します。

| 名前             | 種類                                     | 必須 | 説明                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 電子メール            | string                                   | 〇      | 顧客の電子メールアドレス。                                                                                                                                                                                   |
| カルチャ          | string                                   | 〇      | "En-us" など、コミュニケーションおよび通貨に適したカルチャ。 サポートされているカルチャについては、[パートナーセンターのサポートされている言語とロケール](partner-center-supported-languages-and-locales.md) |
| 言語         | string                                   | 〇      | 既定の言語です。 2文字の言語コード (en、fr など) がサポートされています。                                                                                                                                |
| 会社の\_名    | string                                   | 〇      | 登録されている会社名または組織名。                                                                                                                                                                       |
| 既定の\_アドレス | [先](utility-resources.md#address) | 〇      | 顧客の会社/組織の登録済みアドレス。 すべての長さの制限については、[アドレス](utility-resources.md#address)リソースを参照してください。                                             |

#### <a name="company-profile"></a>会社のプロファイル

次の表では、新しい顧客を作成するために必要な、ユーザーの会社の[プロファイル](customer-resources.md#customercompanyprofile)リソースの最低限必要なフィールドについて説明します。

| 名前   | 種類   | 必須 | 説明                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| domain | string | .うん     | 顧客のドメイン名 (contoso.onmicrosoft.com など)。 |

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 823
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": null,
    "CommerceId": null,
    "CompanyProfile": {
        "TenantId": null,
        "Domain": "WingtipToys678152504.onmicrosoft.com",
        "CompanyName": null,
        "Attributes": {
            "ObjectType": "CustomerCompanyProfile"
        }
    },
    "BillingProfile": {
        "Id": null,
        "FirstName": null,
        "LastName": null,
        "Email": "Gena@wingtiptoys.com",
        "Culture": "EN-US",
        "Language": "En",
        "CompanyName": "Wingtip Toys678152504",
        "DefaultAddress": {
            "Country": "US",
            "Region": null,
            "City": "Redmond",
            "State": "WA",
            "AddressLine1": "One Microsoft Way",
            "AddressLine2": null,
            "PostalCode": "98052",
            "FirstName": "Gena",
            "LastName": "Soto",
            "PhoneNumber": "4255550101"
        },
        "Attributes": {
            "ObjectType": "CustomerBillingProfile"
        }
    },
    "RelationshipToPartner": "none",
    "AllowDelegatedAccess": null,
    "UserCredentials": null,
    "CustomDomains": null,
    "AssociatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "Attributes": {
        "ObjectType": "Customer"
    }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答には新しい顧客の[顧客](customer-resources.md#customer)リソースが含まれます。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 201 Created
Content-Length: 1085
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CV: Yy/YaA0gYEmfQyR/.0
MS-ServerId: 030020525
Date: Tue, 06 Jun 2017 23:11:40 GMT

{
    "id": "626099fe-17af-4756-9fd0-6a73b7127859",
    "commerceId": "626099fe-17af-4756-9fd0-6a73b7127859",
    "companyProfile": {
        "tenantId": "626099fe-17af-4756-9fd0-6a73b7127859",
        "domain": "WingtipToys678152504.onmicrosoft.com",
        "companyName": "Wingtip Toys678152504",
        "links": {
            "self": {
                "uri": "/customers/626099fe-17af-4756-9fd0-6a73b7127859/profiles/company",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "7079246e-7b62-56ef-7cbd-a819514b54b5",
        "email": "Gena@wingtiptoys.com",
        "culture": "en-US",
        "language": "En",
        "companyName": "Wingtip Toys678152504",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Gena",
            "lastName": "Soto",
            "phoneNumber": "4255550101"
        },
        "attributes": {
            "etag": "-8799889149591823008",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "reseller",
    "allowDelegatedAccess": true,
    "userCredentials": {
        "userName": "admin",
        "password": "0Krha*Io"
    },
    "associatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "attributes": {
        "objectType": "Customer"
    }
}
```