---
title: Microsoft 顧客契約の契約メタデータを取得する
description: この記事では、Microsoft カスタマーアグリーメントの契約メタデータを取得する方法について説明します。
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 45cc1284d872072a80a973cfee5a6218452a2409
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096966"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Microsoft 顧客契約の契約メタデータを取得する

**適用対象:**

- パートナー センター

Microsoft カスタマーアグリーメントの契約メタデータは、現在、 *microsoft パブリッククラウド*のパートナーセンターでのみサポートされています。 次の場合には適用されません。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

次のことを行うには、事前に Microsoft Customer Agreement の契約メタデータを取得しておく必要があります。

- [お客様が Microsoft カスタマーアグリーメントに同意したことを確認する](./confirm-customer-consent-customer-agreement.md)
- [Microsoft カスタマーアグリーメントテンプレートのダウンロードリンクを取得する](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>前提条件

- パートナー センター .NET SDK を使用している場合、バージョン 1.14 以降が必要です。

- [パートナー センターの認証](./partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザー認証のみがサポートされます。

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

| 認証方法 | 要求 URI                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [* \{ baseURL \} *](partner-center-rest-urls.md)/v1/agreements? agreementType = {AGREEMENT-type} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

| 名前                   | Type     | 必須 | 説明                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| 契約タイプ | string | いいえ | このパラメーターを使用して、特定のアグリーメントの種類に対するクエリ応答のスコープを指定します。 サポートされる値は <ul><li>Microsoft の種類の**契約に含まれる契約**メタデータのみを含む Microsoft *cloudagreement*</li><li>Microsoft の**顧客契約**では、契約メタデータのみが含まれて*います。*</li><li>**\*** すべてのアグリーメントメタデータを返します。 (を使用しないで **\*** ください。ただし、お使いのコードに、不明な契約の種類を処理するために必要なランタイムロジックがある場合を除きます)。</li></ul> URI パラメーターが指定されていない場合、クエリは、旧バージョンとの互換性のために、既定では**Microsoft Cloudagreement**に設定されます。  |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

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

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。

このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

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
