---
title: Microsoft 顧客契約へのお客様の同意を確認する
description: Microsoft 顧客契約に対するお客様の同意を確認します。
ms.date: 02/04/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 2f59616191a4ce255a294e9c80c26a4e73eda267
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82154404"
---
# <a name="confirm-customer-acceptance-of-microsoft-customer-agreement"></a>Microsoft 顧客契約へのお客様の同意を確認する

**適用対象:**

- パートナー センター

現在、パートナー センターでは、Microsoft 顧客契約に対するお客様の同意の確認を、*Microsoft パブリック クラウド*でのみサポートしています。 この機能は現在、以下には適用されません。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

この記事では、Microsoft 顧客契約に対する顧客の同意を確認または再確認する方法について説明します。

## <a name="prerequisites"></a>前提条件

- パートナー センター .NET SDK を使用している場合、バージョン 1.14 以降が必要です。

- [パートナー センターの認証](./partner-center-authentication.md)に関するページで説明している資格情報。 *このシナリオでは、アプリとユーザー認証のみがサポートされます。*

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- 顧客が Microsoft 顧客契約に同意したときの日付 (**dateAgreed**)。

- Microsoft 顧客契約に同意した顧客組織のユーザーに関する情報。 たとえば、次のようなアニメーションや効果を作成できます。
  - 名
  - 姓
  - 電子メール アドレス
  - 電話番号 (オプション)

## <a name="net"></a>.NET

Microsoft 顧客契約に対する顧客の同意を確認または再確認するには、次のようにします。

1. Microsoft 顧客契約の契約メタデータを取得します。 Microsoft 顧客契約の **templateId** を取得する必要があります。 詳細については、「[Microsoft 顧客契約の契約メタデータを取得する](get-customer-agreement-metadata.md)」を参照してください。

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. 確認の詳細を含む新しい **Agreement** オブジェクトを作成します。

3. **IAgreggatePartner** コレクションを使用して、指定された **customer-tenant-id** で **ById** メソッドを呼び出します。

4. **Agreements** プロパティを使用し、**Create** または **CreateAsync** を呼び出します。

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

完全なサンプルについては、[コンソール テスト アプリ](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) プロジェクトの [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) クラスを参照してください。

## <a name="rest-request"></a>REST 要求

Microsoft 顧客契約に対する顧客の同意を確認または再確認するには、次のようにします。

1. Microsoft 顧客契約の契約メタデータを取得します。 Microsoft 顧客契約の **templateId** を取得する必要があります。 詳細については、「[Microsoft 顧客契約の契約メタデータを取得する](get-customer-agreement-metadata.md)」を参照してください。

2. 顧客が Microsoft 顧客契約に同意していることを確認するために新しい [**Agreement**リソース](agreement-resources.md)を作成します。 次の [REST 要求構文](#request-syntax)を使用します。

### <a name="request-syntax"></a>要求の構文

| 認証方法 | 要求 URI                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

次のクエリ パラメーターを使用して、確認する顧客を指定します。

| 名前               | 種類 | 必須 | 説明                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | はい | この値は、顧客を指定できるようにする識別子である、GUID 形式の **customer-tenant-id** です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

次の表では、REST 要求本文の必須プロパティについて説明しています。

| 名前      | 種類   | 説明                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| 契約 | オブジェクト | Microsoft 顧客契約に対する顧客の同意を確認するためにパートナーにより指定される詳細。 |

#### <a name="agreement"></a>契約

次の表では、[**Agreement** リソース](agreement-resources.md)を作成するために最低限必要なフィールドについて説明します。

| プロパティ       | 種類   | 説明                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Contact](./utility-resources.md#contact) | Microsoft 顧客契約に同意した顧客組織のユーザーに関する情報 (**firstName**、**lastName**、**email**、**phoneNumber** (省略可能)) |
| dateAgreed     | UTC 日時形式の文字列 |顧客が契約に同意した日付。 |
| templateId     | string | 顧客が同意した契約の種類を表す一意の識別子。 Microsoft 顧客契約の契約メタデータを取得することで、Microsoft 顧客契約の **templateId** を取得できます。 詳細については、「[Microsoft 顧客契約の契約メタデータを取得する](./get-customer-agreement-metadata.md)」を参照してください。 |
| 型           | string | 顧客が同意した契約の種類。 顧客が Microsoft 顧客契約に同意している場合には、"MicrosoftCustomerAgreement" を使用します。 |

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

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは [**Agreement** リソース](./agreement-resources.md)を返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。

このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

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
