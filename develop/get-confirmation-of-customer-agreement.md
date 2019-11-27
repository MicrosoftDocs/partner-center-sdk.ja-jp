---
title: Microsoft カスタマーアグリーメントに対する顧客の同意を確認する
description: このトピックでは、お客様が Microsoft カスタマーアグリーメントに同意したかどうかを確認する方法について説明します。
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7b25e48955ed8fb89934c5296492a9525154c264
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486592"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>Microsoft カスタマーアグリーメントに対する顧客の同意を確認する

適用対象:

- パートナー センター

現在、**アグリーメント**リソースは、 *Microsoft パブリッククラウド*のパートナーセンターでのみサポートされています。 このリソースはに適用されません:

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

この記事では、お客様が Microsoft カスタマーアグリーメントに同意したかどうかを確認する方法について説明します。

## <a name="prerequisites"></a>前提条件

- パートナーセンター .NET SDK を使用している場合は、バージョン1.14 以降が必要です。
- 「[パートナーセンターの認証](./partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリとユーザー認証のみがサポートされます。
- 顧客識別子 (**顧客-テナント id**)。

## <a name="net"></a>.NET

以前に提供された顧客の同意の確認を取得するには、次のようにします。

- **Iaggregatepartner.customers**コレクションを使用し、指定された顧客識別子を使用して**ById**メソッドを呼び出します。
- **ByAgreementType**メソッドを呼び出して、**アグリーメント**のプロパティを取得し、結果を Microsoft Customer Agreement にフィルター処理します。
- **Get**または**GetAsync**メソッドを呼び出します。

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

完全なサンプルは、[コンソールテストアプリ](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)プロジェクトの[get顧客契約](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs)クラスにあります。


## <a name="rest-request"></a>REST 要求

以前に提供された顧客の同意の確認を取得するには、次のようにします。

1. REST 要求を作成して、顧客の[契約](./agreement-resources.md)コレクションを取得します。 
2. **AgreementType**クエリパラメーターを使用して、結果の範囲を Microsoft Customer Agreement のみに限定します。

### <a name="request-syntax"></a>要求の構文

次の要求構文を使用します。

| メソッド | 要求 URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/V1/customers/{customer-tenant-id}/agreements? agreementType = {agreement-TYPE} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

要求では、次の URI パラメーターを使用できます。

| 名前             | 種類 | 必須 | 説明                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| 顧客-テナント id | GUID | 〇 | 値は、顧客を指定できるようにする GUID 形式の顧客**tenantid**です。 |
| 契約タイプ | string | X | このパラメーターは、すべてのアグリーメントメタデータを返します。 このパラメーターを使用して、特定のアグリーメントの種類に対するクエリ応答のスコープを指定します。 サポートされている値は次のとおりです。 <ul><li>Microsoft の**Cloudagreement**では、種類が " *microsoft*" の契約のメタデータのみが含まれています。</li><li>Microsoft の**顧客契約**では、種類が「 *Microsoft の顧客契約*」の契約メタデータのみが含まれています。</li><li>すべてのアグリーメントメタデータを返す **\*** 。 (予期しない契約の種類を処理するために必要なロジックがコードに含まれていない場合は、 **\*** を使用しないでください)。</li></ul> URI パラメーターが指定されていない場合、クエリは、旧バージョンとの互換性のために、既定では**Microsoft Cloudagreement**に設定されます。 Microsoft では、契約のメタデータをいつでも新しい契約の種類と共に導入する場合があります。  |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>要求本文

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で**アグリーメント**リソースのコレクションを返します。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 

ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

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
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
