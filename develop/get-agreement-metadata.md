---
title: Microsoft Cloud 契約の契約メタデータを取得する
description: この記事では、Microsoft Cloud Agreement のアグリーメントメタデータを取得する方法について説明します。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 909dec77dd189005839d72caeb0e66a7ad5c8a1b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097151"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Microsoft Cloud 契約の契約メタデータを取得する

**適用対象**

- パートナー センター

> [!NOTE]
> **AgreementMetaData**リソースは、現在、Microsoft パブリッククラウドのパートナーセンターでのみサポートされています。 次の場合には適用されません。
> - 21Vianet が運営するパートナー センター
> - Microsoft Cloud ドイツのパートナー センター
> - 米国政府機関向け Microsoft Cloud のパートナー センター

## <a name="prerequisites"></a>必須コンポーネント

- パートナーセンター .NET SDK を使用している場合は、バージョン1.9 以降が必要です。

- パートナーセンターの Java SDK を使用している場合は、バージョン1.8 以降が必要です。

- [パートナー センターの認証](./partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリ + ユーザー認証がサポートされています。

## <a name="net-version-114-or-newer"></a>.NET (バージョン1.14 以降)

Microsoft Cloud Agreement のアグリーメントメタデータを取得するには:

1. まず、 **AgreementDetails**コレクションを取得します。

2. **ByAgreementType**メソッドを呼び出して、コレクションを Microsoft Cloud Agreement にフィルター処理します。

3. 最後に、 **Get**または**GetAsync**メソッドを呼び出します。

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

完全なサンプルは、[コンソールテストアプリ](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)プロジェクトの[GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs)クラスにあります。

## <a name="net-version-19---113"></a>.NET (バージョン 1.9-1.13)

Microsoft Cloud Agreement のアグリーメントメタデータを取得するには:

まず**Iaggregatepartner.customers AgreementDetails**コレクションを取得し、 **Get**または**GetAsync**メソッドを呼び出します。 次に、コレクション内の項目を検索します。これは Microsoft Cloud アグリーメントに対応しています。

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Microsoft Cloud Agreement のアグリーメントメタデータを取得するには:

まず、 **iaggregatepartner.customers**関数を呼び出し、次に**get**関数を呼び出します。 次に、コレクション内の項目を検索します。これは Microsoft Cloud アグリーメントに対応しています。

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

完全なサンプルは、[コンソールテストアプリ](https://github.com/Microsoft/Partner-Center-Java-Samples)プロジェクトの[GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java)クラスにあります。

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Microsoft Cloud Agreement のアグリーメントメタデータを取得するには:

[**PartnerAgreementDetail**](https://docs.microsoft.com/powershell/module/partnercenter/get-partneragreementdetail)コマンドを使用します。 次に、コレクション内の項目を検索します。これは Microsoft Cloud アグリーメントに対応しています。

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a>REST 要求

Microsoft Cloud Agreement のアグリーメントメタデータを取得するには、まず REST 要求を作成して**AgreementMetaData** collection を取得します。 次に、Microsoft Cloud Agreement に対応するコレクション内の項目を検索します。

### <a name="request-syntax"></a>要求の構文

| 認証方法 | 要求 URI                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [* \{ BASEURL \} *](partner-center-rest-urls.md)/v1/agreements HTTP/1.1 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で**AgreementMetaData**リソースのコレクションを返します。

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

応答で Microsoft Cloud アグリーメントに対応するリソースを特定するには、 **agreementType**プロパティの値が "Microsoft cloudagreement" であるリソースを探します。
