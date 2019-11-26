---
title: Microsoft Cloud 契約の契約メタデータを取得する
description: This topic explains how to get agreement metadata for Microsoft Cloud Agreement.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0608a735705e02fe70ceabfd60d33cda6a9e4d0e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486102"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Microsoft Cloud 契約の契約メタデータを取得する

**Applies To**

- パートナー センター

> [!NOTE]  
> The **AgreementMetaData** resource is currently supported by Partner Center in the Microsoft public cloud only. 以下には適用されません。
> - 21Vianet が運営するパートナー センター
> - Microsoft Cloud ドイツのパートナー センター
> - 米国政府機関向け Microsoft Cloud のパートナー センター

## <a name="prerequisites"></a>前提条件

- If you are using the Partner Center .NET SDK, version 1.9 or newer is required.
- If you are using the Partner Center Java SDK, version 1.8 or newer is required.
- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario supports app + user authentication..

## <a name="net-version-114-or-newer"></a>.NET (version 1.14 or newer)

To retrieve the agreement metadata for Microsoft Cloud Agreement:

1. First, retrieve the **IAggregatePartner.AgreementDetails** collection.

2. Call **ByAgreementType** method to filter the collection to Microsoft Cloud Agreement.

3. Finally, call **Get** or **GetAsync** method.

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.

## <a name="net-version-19---113"></a>.NET (version 1.9 - 1.13)

To retrieve agreement metadata for the Microsoft Cloud Agreement:

First retrieve the **IAggregatePartner.AgreementDetails** collection and then call the **Get** or **GetAsync** methods. Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

To retrieve agreement metadata for the Microsoft Cloud Agreement:

First call the **IAggregatePartner.getAgreementDetails** function and then call the **get** function. Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:

```java
// IAggregatePartner partnerOperations;

ResourceCollection<AgreementMetaData> agreements = partnerOperations.getAgreements().get();

AgreementMetaData microsoftCloudAgreement;

for (AgreementMetaData metadata : agreements)
{
    if(metadata.getAgreementType() == AgreementType.MicrosoftCloudAgreement)
    {
        microsoftCloudAgreement = metadata;
    }
}
```

A complete sample can be found in the [GetAgreementDetails](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

To retrieve agreement metadata for the Microsoft Cloud Agreement:

Use the [**Get-PartnerAgreementDetail**](https://docs.microsoft.com/powershell/module/partnercenter/partner-center/get-partneragreementdetail) command. Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest"></a>REST

### <a name="rest-request"></a>REST request

To retrieve agreement metadata for Microsoft Cloud Agreement, first create a REST Request to retrieve the **AgreementMetaData** collection. Then search for the item in the collection which corresponds to the Microsoft Cloud Agreement.

#### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/agreements HTTP/1.1 |

#### <a name="request-headers"></a>要求ヘッダー

- See [Partner Center REST headers](headers.md) for more information.

#### <a name="request-body"></a>要求本文

なし。

#### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

### <a name="rest-response"></a>REST response

If successful, this method returns a collection of **AgreementMetaData** resources in the response body.

#### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

#### <a name="response-example"></a>応答の例

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
            "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
            "agreementType": "MicrosoftCloudAgreement",
            "agreementLink": "https://docs.microsoft.com/partner-center/agreements",
            "versionRank": 0
        }
    ],
    "links": {
        "self": {
            "uri": "/agreements",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

To identify the resource in the response which corresponds to the Microsoft Cloud Agreement, look for the resource whose **agreementType** property has value "MicrosoftCloudAgreement".

---
