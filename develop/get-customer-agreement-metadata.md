---
title: Get agreement metadata for the Microsoft Customer Agreement
description: This topic explains how to get agreement metadata for Microsoft Customer Agreement.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 999c2c4cb6146dd62faffbd93f73e5721e019004
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485672"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Get agreement metadata for the Microsoft Customer Agreement

適用対象:

- パートナー センター

Agreement metadata for Microsoft Customer Agreement is currently supported by Partner Center only in the *Microsoft public cloud*. It doesn't apply to:

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

You must retrieve the agreement metadata for the Microsoft Customer Agreement before you can:

- [Confirm a customer's acceptance of the Microsoft Customer Agreement](./confirm-customer-consent-customer-agreement.md)
- [Retrieve a download link for the Microsoft Customer Agreement template](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>前提条件

- If you are using the Partner Center .NET SDK, version 1.14 or newer is required.
- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario supports App+User authentication only.


## <a name="net-version-114-or-newer"></a>.NET (version 1.14 or newer)

To retrieve the agreement metadata for Microsoft Customer Agreement:

1. First, retrieve the **IAggregatePartner.AgreementDetails** collection.

2. Call **ByAgreementType** method to filter the collection to Microsoft Customer Agreement.

3. Finally, call **Get** or **GetAsync** method.

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.


## <a name="rest-request"></a>REST request

To retrieve the agreement metadata for Microsoft Customer Agreement:

1. Create a REST request to retrieve the [AgreementMetaData](./agreement-metadata-resources.md) collection.
2. Use the **agreementType** query parameter to scope the result to only the Microsoft Customer Agreement.

### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

| 名前                   | タスクバーの検索ボックスに     | 必須かどうか | 説明                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| agreement-type | string | 必須ではない | Use this parameter to scope the query response to specific agreement type. The supported values are: <ul><li>**MicrosoftCloudAgreement** that includes agreement metadata only of the type *MicrosoftCloudAgreement*</li><li>**MicrosoftCustomerAgreement** that includes agreement metadata only of the type *MicrosoftCustomerAgreement*.</li><li>**\*** that returns all agreement metadata. (Don't use **\*** unless your code has the necessary runtime logic to handle unfamiliar agreement types because Microsoft may introduce agreement metadat with new agreement types at any time.)</li></ul> If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.  |

### <a name="request-headers"></a>要求ヘッダー

For more information, see [Partner Center REST headers](headers.md).

### <a name="request-body"></a>要求本文

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST response

If successful, this method returns a collection of [**AgreementMetaData** resources](./agreement-metadata-resources.md) in the response body.

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
    "totalCount": 1,
    "items": [
        {
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
