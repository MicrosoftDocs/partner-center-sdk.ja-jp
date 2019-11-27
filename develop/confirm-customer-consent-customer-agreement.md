---
title: Microsoft カスタマーアグリーメントに同意するかどうかを確認する
description: お客様による Microsoft カスタマーアグリーメントへの同意を確認します。
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7c7c3acea0f2e45b53fde7372bbb1f33fcb9de13
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488952"
---
# <a name="confirm-customer-acceptance-of-microsoft-customer-agreement"></a>Microsoft カスタマーアグリーメントに同意するかどうかを確認する

適用対象:

- パートナー センター

現在、パートナーセンターでは、microsoft*パブリッククラウド*でのみ、Microsoft カスタマー契約に対する顧客からの同意の確認をサポートしています。 現在、この機能は次の対象には適用されません。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

この記事では、Microsoft カスタマーアグリーメントに対する顧客の同意を確認または再確認する方法について説明します。

## <a name="prerequisites"></a>前提条件

- パートナーセンター .NET SDK を使用している場合は、バージョン1.14 以降が必要です。
- 「[パートナーセンターの認証](./partner-center-authentication.md)」で説明されている資格情報。 *このシナリオでは、アプリとユーザー認証のみがサポートされます。*
- 顧客識別子 (**顧客-テナント id**)。
- 顧客が Microsoft カスタマーアグリーメントに同意した日付 (**dateagreed**)。
- Microsoft カスタマーアグリーメントに同意した顧客組織のユーザーに関する情報。 たとえば、次のようなアニメーションや効果を作成できます。
  - 名
  - 姓
  - メール アドレス
  - 電話番号 (オプション)

## <a name="net"></a>.NET

Microsoft カスタマーアグリーメントに同意するかどうかを確認または再確認するには:

1. Microsoft カスタマーアグリーメントの契約メタデータを取得します。 Microsoft カスタマーアグリーメントの**templateId**を取得する必要があります。 詳細については、「 [Microsoft Customer agreement の契約メタデータを取得する](get-customer-agreement-metadata.md)」を参照してください。

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. 確認の詳細を含む新しい**アグリーメント**オブジェクトを作成します。
3. **IAgreggatePartner**コレクションを使用し、指定された**顧客テナント id**を使用して**ById**メソッドを呼び出します。
4. **[アグリーメント]** プロパティを使用し、次に**Create**または**createasync**を呼び出します。

```csharp
// string selectedCustomerId;

var agreementToCreate = new Agreement
{
    DateAgreed = DateTime.UtcNow,
    TemplateId = microsoftCustomerAgreementDetails.TemplateId,
    PrimaryContact = new Contact
    {
        FirstName = "Tania",
        LastName = "Carr",
        Email = "someone@example.com",
        PhoneNumber = "1234567890"
    }
};

Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
```

完全なサンプルは、[コンソールテストアプリ](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)プロジェクトの[CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs)クラスにあります。


## <a name="rest-request"></a>REST 要求

Microsoft カスタマーアグリーメントに同意するかどうかを確認または再確認するには:

1. Microsoft カスタマーアグリーメントの契約メタデータを取得します。 Microsoft カスタマーアグリーメントの**templateId**を取得する必要があります。 詳細については、「 [Microsoft Customer agreement の契約メタデータを取得する](get-customer-agreement-metadata.md)」を参照してください。
2. 新しい[**契約**リソース](agreement-resources.md)を作成して、顧客が Microsoft カスタマーアグリーメントに同意したことを確認します。 次の[REST 要求構文](#request-syntax)を使用します。

### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを使用して、確認する顧客を指定します。

| 名前               | 種類 | 必須 | 説明                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| 顧客-テナント id | GUID | 〇 | 値は、GUID 形式の**顧客テナント id**です。これは、顧客を指定するための識別子です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>要求本文

次の表では、REST 要求本文の必須プロパティについて説明します。

| 名前      | 種類   | 説明                                                                                  |  
|-----------|--------|----------------------------------------------------------------------------------------------|  
| 契約 | オブジェクト | パートナーによって提供される、Microsoft カスタマーアグリーメントに対する顧客の同意を確認するための詳細。 |  

#### <a name="agreement"></a>契約

次の表では、 [**アグリーメント**リソース](agreement-resources.md)を作成するために必要な最小限のフィールドについて説明します。

| プロパティ       | 種類   | 説明                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Contact](./utility-resources.md#contact) | Microsoft Cloud 契約に同意したお客様の組織のユーザーに関する情報: **firstName**、 **lastName**、 **email** 、 **phoneNumber** (省略可能) |
| dateAgreed     | UTC 日時形式の文字列 |顧客がアグリーメントに同意した日付。 |
| templateId     | string | 顧客が受け入れるアグリーメントの種類を表す一意の識別子。 Microsoft Customer Agreement の契約メタデータを取得することによって、 **templateId** For Microsoft customer agreement を取得できます。 詳細については、「 [Microsoft Cloud agreement のアグリーメントメタデータの取得](./get-customer-agreement-metadata.md)」を参照してください。 |
| type           | string | 顧客が受け入れる契約の種類。 お客様が Microsoft カスタマーアグリーメントに同意した場合は、"microsoft の顧客契約" を使用します。 |
  
#### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

### <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは[**アグリーメント**リソース](./agreement-resources.md)を返します。

#### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 

ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

#### <a name="response-example"></a>応答の例

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
