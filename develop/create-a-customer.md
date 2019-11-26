---
title: 顧客の作成
description: 新しい顧客を作成する方法。
ms.assetid: 7EA3E23F-0EA8-49CB-B98A-C4B74F559873
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 94ce486779ca53d27d7a53a5277060324b7acc23
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489332"
---
# <a name="create-a-customer"></a>顧客の作成

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

このトピックでは、新しい顧客を作成する方法について説明します。

> [!IMPORTANT]
> 間接的なプロバイダーの場合、間接リセラーの顧客を作成するには、「[間接リセラーの顧客を作成](create-a-customer-for-an-indirect-reseller.md)する」を参照してください。

クラウドソリューションプロバイダー (CSP) パートナーは、顧客を作成するときに、顧客に代わって注文を行うことができます。 顧客を作成するときに、次のものも作成します。

- 顧客の Azure Active Directory (AD) テナントオブジェクト。
- 代理管理者特権に使用される、リセラーと顧客の間の関係。
- 顧客の管理者としてサインインするためのユーザー名とパスワード。

顧客が作成されたら、パートナーセンター SDK (たとえば、アカウント管理) で今後使用するために、顧客 ID と Azure AD の詳細を保存してください。

## <a name="prerequisites"></a>前提条件

「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

> [!IMPORTANT]
> 顧客テナントを作成するには、作成プロセス中に有効な物理アドレスを指定する必要があります。 アドレスを検証するには、「[アドレスの検証](validate-an-address.md)」の手順に従ってください。 サンドボックス環境で無効なアドレスを使用して顧客を作成した場合、その顧客のテナントを削除することはできません。

## <a name="c"></a>C\#

顧客を追加するには:

1. 新しい[**Customer**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer)オブジェクトをインスタンス化します。 この[**プロファイル**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile)と会社の[**プロファイル**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)を必ず入力してください。
2. [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create)または[**createasync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)を呼び出して、新しい顧客を[**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers)コレクションに追加します。

### <a name="c-example"></a>C\# の例

```csharp
// IAggregatePartner partnerOperations;

var partnerOperations = this.Context.UserPartnerOperations;

var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "SampleApplication{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "someone@example.com",
        Language = "En",
        CompanyName = "Some Company" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Tania",
            LastName = "Carr",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = ""
        }
    }
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: CreateCustomer.cs

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

新しい顧客を作成するには:

1. **顧客**企業**プロファイル**オブジェクトの新しいインスタンスを作成します。 必ず必須フィールドに入力してください。
2. **Iaggregatepartner.customers (). create**関数を呼び出して顧客を作成します。

### <a name="java-example"></a>Java の例

```java
// IAggregatePartner partnerOperations;

Address address = new Address();

address.setFirstName( "Gena" );
address.setLastName( "Soto" );
address.setAddressLine1( "One Microsoft Way" );
address.setCity( "Redmond" );
address.setState( "WA" );
address.setCountry( "US" );
address.setPostalCode( "98052" );
address.setPhoneNumber( "4255550101" );

CustomerBillingProfile billingProfile = new CustomerBillingProfile();

billingProfile.setCulture( "en-US" );
billingProfile.setEmail( "gena@wingtiptoys.com" );
billingProfile.setLanguage( "en" );
billingProfile.setCompanyName( "Wingtip Toys" + new Random().nextInt() );
billingProfile.setDefaultAddress( address );

CustomerCompanyProfile companyProfile = new CustomerCompanyProfile();

companyProfile.setDomain( "WingtipToys" + Math.abs( new Random().nextInt() ) + ".onmicrosoft.com" );

Customer customerToCreate = new Customer();

customerToCreate.setBillingProfile( billingProfile );
customerToCreate.setCompanyProfile( companyProfile );

Customer newCustomer = partnerOperations.getCustomers().create( customerToCreate );
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

顧客を作成するには、[**新しい-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md)コマンドを実行します。

### <a name="powershell-example"></a>Powershell の例

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド   | 要求 URI                                                       |
|----------|-------------------------------------------------------------------|
| **投稿** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### <a name="request-headers"></a>要求ヘッダー

- この API はべき等です (複数回呼び出すと、異なる結果が生成されることはありません)。
- 要求 ID と相関 ID が必要です。
- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

次の表では、要求本文に必要なプロパティについて説明します。

| 名前                              | 種類   | 説明                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile](#billing-profile) | オブジェクト | 顧客の請求プロファイル情報。 |
| [会社のプロファイル](#company-profile) | オブジェクト | 顧客の会社のプロファイル情報。 |

#### <a name="billing-profile"></a>課金プロファイル

次の表では、新しい顧客を作成するために必要な、ユーザーごとの[プロファイル](customer-resources.md#customerbillingprofile)リソースの最小限の必須フィールドについて説明します。

| 名前             | 種類                                     | 説明                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 電子メール            | string                                   | 顧客の電子メールアドレス。                                                                                                                                                                                   |
| カルチャ          | string                                   | "En-us" など、コミュニケーションおよび通貨に適したカルチャ。 サポートされているカルチャについては、[パートナーセンターのサポートされている言語とロケール](partner-center-supported-languages-and-locales.md) |
| 言語         | string                                   | 既定の言語です。 2文字の言語コード (en、fr など) がサポートされています。                                                                                                                                |
| 会社の\_名    | string                                   | 登録されている会社名または組織名。                                                                                                                                                                       |
| 既定の\_アドレス | [先](utility-resources.md#address) | 顧客の会社/組織の登録済みアドレス。 すべての長さの制限については、[アドレス](utility-resources.md#address)リソースを参照してください。                                             |

#### <a name="company-profile"></a>会社のプロファイル

次の表では、新しい顧客を作成するために必要な、ユーザーの会社の[プロファイル](customer-resources.md#customercompanyprofile)リソースの最低限必要なフィールドについて説明します。

| 名前   | 種類   | 説明                                                  |
|--------|--------|--------------------------------------------------------------|
| domain | string | 顧客のドメイン名 (contoso.onmicrosoft.com など)。 |

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "CompanyProfile": {
        "Domain": "xyz.ccsctp.net",
    },
    "BillingProfile": {
        "Culture": "EN-US",
        "Email": "test@outlook.com",
        "Language": "en",
        "CompanyName": "test company",
        "DefaultAddress": {
            "FirstName": "Test",
            "LastName": "Test",
            "AddressLine1": "One Microsoft Way",
            "City": "Redmond",
            "State": "WA",
            "PostalCode": "98052",
            "Country": "US",
        }
    }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、この API は新しい顧客の[顧客](customer-resources.md#customer)リソースを返します。 パートナーセンター SDK で今後使用するために、顧客 ID と Azure AD の詳細を保存します。 たとえば、アカウント管理で使用するために必要になります。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CV: ObwhuhD2tUKJoM+Z.0
MS-ServerId: 202010223
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "dfd8cc0a-c592-468c-8461-869a38d24738",
    "commerceId": "0a4ce58a-6f96-4273-8035-d9c7d31b9ba4",
    "companyProfile": {
        "tenantId": "dfd8cc0a-c592-468c-8461-869a38d24738",
        "domain": "xyz.ccsctp.net",
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "d17c0275-da92-5c33-9032-782ef1d0b69b",
        "email": "test@outlook.com",
        "culture": "en-US",
        "language": "en",
        "companyName": "test company",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Test",
            "lastName": "Test",
            "phoneNumber": ""
        },
        "attributes": {
            "etag": "5920358838484612121",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "none",
    "userCredentials": {
        "userName": "admin",
        "password": "=;;n.=s9Z"
    },
    "attributes": {
        "objectType": "Customer"
    }
}
```
