---
title: Microsoft Cloud 契約に関する顧客の同意の確認を取得する
description: この記事では、Microsoft Cloud 契約に対する顧客の同意を確認する方法について説明します。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: d2a6b6d10d07abf8c3565fa568691a44691170e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096975"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a>Microsoft Cloud 契約に関する顧客の同意の確認を取得する

**適用対象**

- パートナー センター

> [!NOTE]
> **アグリーメント**リソースは、現在、Microsoft パブリッククラウドのパートナーセンターでのみサポートされています。 次の場合には適用されません。
>
> - 21Vianet が運営するパートナー センター
> - Microsoft Cloud ドイツのパートナー センター
> - 米国政府機関向け Microsoft Cloud のパートナー センター

## <a name="prerequisites"></a>必須コンポーネント

- パートナーセンター .NET SDK を使用している場合は、バージョン1.9 以降が必要です。

- パートナーセンターの Java SDK を使用している場合は、バージョン1.8 以降が必要です。

- [パートナー センターの認証](./partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでサポートされるのは、アプリとユーザー認証のみです。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="net-version-14-or-newer"></a>.NET (バージョン1.4 以降)

以前に提供された顧客の同意の確認を取得するには、次のようにします。

- **Iaggregatepartner.customers**コレクションを使用し、指定された顧客識別子を使用して**ById**メソッドを呼び出します。

- **ByAgreementType**メソッドを呼び出して、**アグリーメント**のプロパティを取得し、結果を Microsoft Cloud agreement にフィルター処理します。

- **Get**または**GetAsync**メソッドを呼び出します。

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

完全なサンプルは、[コンソールテストアプリ](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)プロジェクトの[get顧客契約](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs)クラスにあります。

## <a name="net-version-19---113"></a>.NET (バージョン 1.9-1.13)

以前に提供された顧客の受け入れの確認を取得するには:

**Iaggregatepartner.customers**コレクションを使用し、指定された顧客の識別子を使用して**ById**メソッドを呼び出します。 次に、 **agreement**プロパティを取得し、次に**get**メソッドまたは**GetAsync**メソッドを呼び出します。

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

以前に提供された顧客の受け入れの確認を取得するには:

**Iaggregatepartner.customers**関数を使用し、指定された顧客の識別子を使用して**byId**関数を呼び出します。 次に、 **Getagreements**関数を取得し、次に**get**関数を呼び出します。

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

完全なサンプルは、[コンソールテストアプリ](https://github.com/Microsoft/Partner-Center-Java-Samples)プロジェクトの[get顧客契約](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java)クラスにあります。

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

以前に提供された顧客の受け入れの確認を取得するには:

[**Get Partnerの顧客契約**](https://docs.microsoft.com/powershell/module/partnercenter/get-partnercustomeragreement)コマンドを使用します。

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a>REST 要求

以前に提供された顧客の受け入れの確認を取得するには、次の手順を参照してください。

関連する証明**書**情報を使用して、新しい契約リソースを作成します。

### <a name="request-syntax"></a>要求の構文

| 認証方法 | 要求 URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを使用して、確認する顧客を指定します。

| 名前             | Type | 必須 | 説明                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| 顧客 Tenantid | GUID | Y        | 値は、顧客を指定できるようにする GUID 形式の顧客**tenantid**です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で**アグリーメント**リソースのコレクションを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```
