---
title: Microsoft カスタマーアグリーメントの契約メタデータを取得する
description: このトピックでは、Microsoft カスタマーアグリーメントの契約メタデータを取得する方法について説明します。
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
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Microsoft カスタマーアグリーメントの契約メタデータを取得する

適用対象:

- パートナー センター

Microsoft カスタマーアグリーメントの契約メタデータは、現在、 *microsoft パブリッククラウド*のパートナーセンターでのみサポートされています。 次の場合には適用されません。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

次のことを行うには、事前に Microsoft Customer Agreement の契約メタデータを取得しておく必要があります。

- [お客様が Microsoft カスタマーアグリーメントに同意したことを確認する](./confirm-customer-consent-customer-agreement.md)
- [Microsoft カスタマーアグリーメントテンプレートのダウンロードリンクを取得する](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>前提条件

- パートナーセンター .NET SDK を使用している場合は、バージョン1.14 以降が必要です。
- 「[パートナーセンターの認証](./partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリとユーザー認証のみがサポートされます。


## <a name="net-version-114-or-newer"></a>.NET (バージョン1.14 以降)

Microsoft Customer Agreement の契約メタデータを取得するには:

1. まず、 **AgreementDetails**コレクションを取得します。

2. **ByAgreementType**メソッドを呼び出して、コレクションを Microsoft カスタマーアグリーメントにフィルター処理します。

3. 最後に、 **Get**または**GetAsync**メソッドを呼び出します。

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

完全なサンプルは、[コンソールテストアプリ](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)プロジェクトの[GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs)クラスにあります。


## <a name="rest-request"></a>REST 要求

Microsoft Customer Agreement の契約メタデータを取得するには:

1. [AgreementMetaData](./agreement-metadata-resources.md) collection を取得する REST 要求を作成します。
2. **AgreementType**クエリパラメーターを使用して、結果の範囲を Microsoft Customer Agreement のみに限定します。

### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/V1/agreements? agreementType = {agreement-TYPE} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

| 名前                   | 種類     | 必須 | 説明                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| 契約タイプ | string | X | このパラメーターを使用して、特定のアグリーメントの種類に対するクエリ応答のスコープを指定します。 サポートされている値は次のとおりです。 <ul><li>Microsoft の種類の**契約に含まれる契約**メタデータのみを含む Microsoft *cloudagreement*</li><li>Microsoft の**顧客契約**では、契約メタデータのみが含まれて*います。*</li><li>すべてのアグリーメントメタデータを返す **\*** 。 ( **\*** 使用しないでください。マイクロソフトでは、契約の種類を問わず、契約の種類に同意する必要があります。</li></ul> URI パラメーターが指定されていない場合、クエリは、旧バージョンとの互換性のために、既定では**Microsoft Cloudagreement**に設定されます。  |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md)」を参照してください。

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

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で[ **AgreementMetaData**リソース](./agreement-metadata-resources.md)のコレクションを返します。

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
