---
title: Microsoft Cloud 契約に対する顧客の同意を確認する
description: このトピックでは、Microsoft Cloud 契約に対する顧客の同意を確認する方法について説明します。
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 9ae40cd3c9805ee8ddaae6d98fd0d6b61ede8d40
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485662"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a>Microsoft Cloud 契約に関するお客様の同意の確認を取得する

**適用対象**

- パートナー センター

> [!NOTE]  
> **アグリーメント**リソースは、現在、Microsoft パブリッククラウドのパートナーセンターでのみサポートされています。 以下には適用されません。
> - 21Vianet が運営するパートナー センター
> - Microsoft Cloud ドイツのパートナー センター
> - 米国政府機関向け Microsoft Cloud のパートナー センター

## <a name="prerequisites"></a>前提条件

- パートナーセンター .NET SDK を使用している場合は、バージョン1.9 以降が必要です。
- パートナーセンターの Java SDK を使用している場合は、バージョン1.8 以降が必要です。
- 「[パートナーセンターの認証](./partner-center-authentication.md)」で説明されている資格情報。 このシナリオでサポートされるのは、アプリとユーザー認証のみです。
- 顧客 ID (顧客-テナント id)。

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

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

以前に提供された顧客の受け入れの確認を取得するには:

**Iaggregatepartner.customers**関数を使用し、指定された顧客の識別子を使用して**byId**関数を呼び出します。 次に、 **Getagreements**関数を取得し、次に**get**関数を呼び出します。

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

完全なサンプルは、[コンソールテストアプリ](https://github.com/Microsoft/Partner-Center-Java-Samples)プロジェクトの[get顧客契約](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java)クラスにあります。

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

以前に提供された顧客の受け入れの確認を取得するには:

[**Get Partnerの顧客契約**](https://docs.microsoft.com/powershell/module/partnercenter/partner-center/get-partnercustomeragreement)コマンドを使用します。

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest"></a>休息

以前に提供された顧客の受け入れの確認を取得するには、次の手順を参照してください。

### <a name="rest-request"></a>REST 要求

関連する証明**書**情報を使用して、新しい契約リソースを作成します。  

#### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

##### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを使用して、確認する顧客を指定します。

| 名前             | 種類 | 必須 | 説明                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| 顧客 Tenantid | GUID | Y        | 値は、顧客を指定できるようにする GUID 形式の顧客**tenantid**です。 |

#### <a name="request-headers"></a>要求ヘッダー

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

#### <a name="request-body"></a>要求本文

なし。

#### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

### <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で**アグリーメント**リソースのコレクションを返します。

#### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

#### <a name="response-example"></a>応答の例

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

---
