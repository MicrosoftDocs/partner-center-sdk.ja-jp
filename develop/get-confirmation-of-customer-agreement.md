---
title: Get confirmation of customer acceptance of Microsoft Customer Agreement
description: This topic explains how to get confirmation of customer acceptance of the Microsoft Customer Agreement.
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
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>Get confirmation of customer acceptance of Microsoft Customer Agreement

適用対象:

- パートナー センター

The **Agreement** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource doesn't apply to:

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

This article explains how you can retrieve confirmation(s) of a customer's acceptance of the Microsoft Customer Agreement.

## <a name="prerequisites"></a>前提条件

- If you are using the Partner Center .NET SDK, version 1.14 or newer is required.
- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario only supports App+User authentication.
- A customer identifier (**customer-tenant-id**).

## <a name="net"></a>.NET の場合

To retrieve confirmation(s) of customer acceptance that was previously provided:

- Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.
- Fetch the **Agreements** property and filter the results to Microsoft Customer Agreement by calling **ByAgreementType** method.
- Call **Get** or **GetAsync** method.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.


## <a name="rest-request"></a>REST request

To retrieve confirmation of customer acceptance that was previously provided:

1. Create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for the customer. 
2. Use the **agreementType** query parameter to scope the results to only the Microsoft Customer Agreement.

### <a name="request-syntax"></a>要求の構文

Use the following request syntax:

| メソッド | 要求 URI                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

You can use the following URI parameters with your request:

| 名前             | タスクバーの検索ボックスに | 必須かどうか | 説明                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | [はい] | The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer. |
| agreement-type | string | 必須ではない | This parameter returns all agreement metadata. Use this parameter to scope the query response to specific agreement type. The supported values are: <ul><li>**MicrosoftCloudAgreement** that only includes agreement metadata of the type *MicrosoftCloudAgreement*.</li><li>**MicrosoftCustomerAgreement** that only includes agreement metadata of the type *MicrosoftCustomerAgreement*.</li><li>**\*** that returns all agreement metadata. (Don't use **\*** unless your code has the necessary logic to handle unexpected agreement types.)</li></ul> If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility. Microsoft may introduce agreement metadata with new agreement types at any time.  |

### <a name="request-headers"></a>要求ヘッダー

For more information, see [Partner Center REST headers](headers.md).

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

## <a name="rest-response"></a>REST response

If successful, this method returns a collection of **Agreement** resources in the response body.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. 

Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

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
