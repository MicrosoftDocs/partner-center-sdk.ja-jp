---
title: Microsoft Cloud 契約のお客様の同意を確認する
description: Microsoft Cloud 契約に対する顧客の同意を確認する方法。
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b1a0cf111f19d5dc16b000642bcd0b060822369e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488942"
---
# <a name="confirm-customer-acceptance-of-microsoft-cloud-agreement"></a>Microsoft Cloud 契約のお客様の同意を確認する

適用対象:

- パートナー センター

> [!NOTE]  
> **アグリーメント**リソースは、現在、Microsoft パブリッククラウドのパートナーセンターでのみサポートされています。 以下には適用されません。
> - 21Vianet が運営するパートナー センター
> - Microsoft Cloud ドイツのパートナー センター
> - 米国政府機関向け Microsoft Cloud のパートナー センター

Microsoft Cloud 契約に対する顧客の同意を確認する方法。

## <a name="prerequisites"></a>前提条件

- パートナーセンター .NET SDK を使用している場合は、バージョン1.9 以降が必要です。
- パートナーセンターの Java SDK を使用している場合は、バージョン1.8 以降が必要です。
- 「[パートナーセンターの認証](./partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリとユーザー認証のみがサポートされます。
- 顧客 ID (顧客-テナント id)。
- 顧客が Microsoft Cloud 契約に同意した日付。
- Microsoft Cloud 契約に同意した組織のユーザーに関する情報 (以下を含む)。
  - 名
  - 姓
  - メール アドレス
  - 電話番号 (オプション)


## <a name="net-version-114-or-newer"></a>.NET (バージョン1.14 以降)

Microsoft カスタマーアグリーメントに同意するかどうかを確認または再確認するには:

1. Microsoft Cloud 契約のアグリーメントメタデータを取得します。 Microsoft Cloud 契約の**templateId**を取得する必要があります。 詳細については、「 [Microsoft Cloud agreement のアグリーメントメタデータの取得](get-agreement-metadata.md)」を参照してください。

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. 確認の詳細を含む新しい**アグリーメント**オブジェクトを作成します。
3. **IAgreggatePartner**コレクションを使用し、指定された**顧客テナント id**を使用して**ById**メソッドを呼び出します。
4. **[アグリーメント]** プロパティを使用し、次に**Create**または**createasync**を呼び出します。

```csharp
// string selectedCustomerId;

var agreementToCreate = new Agreement
{
    DateAgreed = DateTime.UtcNow,
    TemplateId = microsoftCloudAgreementDetails.TemplateId,
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

## <a name="net-version-19---113"></a>.NET (バージョン 1.9-1.13)

お客様が Microsoft Cloud Agreement に同意したことを確認または再確認するには:

1. Microsoft Cloud 契約のアグリーメントメタデータを取得します。 詳細については、「 [Microsoft Cloud agreement のアグリーメントメタデータの取得](get-agreement-metadata.md)」を参照してください。 Microsoft Cloud Agreement の**TemplateId**を取得するには、この手順が必要です。

    ```csharp
    /// IAggregatePartner partnerOperations;
    var agreements = partnerOperations.AgreementDetails.Get();

    AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
    ```

2. 確認の詳細を含む新しい**アグリーメント**オブジェクトを作成します。 次に、 **iaggregatepartner.customers**コレクションを使用して、指定された顧客の ID で**ById**メソッドを呼び出します。 次に、 **agreement**プロパティを呼び出した後、 **Create**または**createasync**を呼び出します。

    ``` csharp
    // string selectedCustomerId;

    var agreementToCreate = new Agreement
    {
        PrimaryContact = new Contact
        {
            FirstName = "Tania",
            LastName = "Carr",
            Email = "someone@example.com",
            PhoneNumber = "1234567890"
        },
        TemplateId = microsoftCloudAgreement.TemplateId,
        DateAgreed = DateTime.UtcNow,
        Type = AgreementType.MicrosoftCloudAgreement
    };

    Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
    ```

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

お客様が Microsoft Cloud Agreement に同意したことを確認または再確認するには:

1. Microsoft Cloud 契約のアグリーメントメタデータを取得します。 詳細については、「 [Microsoft Cloud agreement のアグリーメントメタデータの取得](get-agreement-metadata.md)」を参照してください。 Microsoft Cloud Agreement の**TemplateId**を取得するには、この手順が必要です。

    ```java
    /// IAggregatePartner partnerOperations;

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

2. 確認の詳細を含む新しい**アグリーメント**オブジェクトを作成します。 次に、 **iaggregatepartner.customers**関数を使用し、指定された顧客の識別子を使用して**byId**関数を呼び出します。 次に、 **Getagreements**プロパティを呼び出した後、 **create**関数を呼び出します。

    ```java
    // String selectedCustomerId;

    Contact primaryContact = new Contact();

    primaryContact.setEmail("someone@example.com");
    primaryContact.setFirstName("Tania");
    primaryContact.setLastName("Carr");
    primaryContact.setPhoneNumber("1234567890");

    Agreement agreementToCreate = new Agreement();

    agreementToCreate.setContact(primaryContact);
    agreementToCreate.setDateAgreed(new DateTime());
    agreementToCreate.setTemplateId(microsoftCloudAgreement.getTemplateId());
    agreementToCreate.setType(AgreementType.MicrosoftCloudAgreement);

    Agreement agreement = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().create(agreementToCreate);
    ```

完全なサンプルは、[コンソールテストアプリ](https://github.com/Microsoft/Partner-Center-Java-Samples)プロジェクトの[CreateCustomerAgreement](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/src/main/java/com/microsoft/store/partnercenter/samples/agreements/CreateCustomerAgreement.java)クラスにあります。

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

お客様が Microsoft Cloud Agreement に同意したことを確認または再確認するには:

1. Microsoft Cloud 契約のアグリーメントメタデータを取得します。 詳細については、「 [Microsoft Cloud agreement のアグリーメントメタデータの取得](get-agreement-metadata.md)」を参照してください。 Microsoft Cloud Agreement の**TemplateId**を取得するには、この手順が必要です。  

    ```powershell  
    $agreement = Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
    ```  

2. [**新しい-Partner顧客契約**](https://docs.microsoft.com/powershell/module/partnercenter/partner-center/new-partnercustomeragreement)コマンドを実行します  

    ```powershell  
    New-PartnerCustomerAgreement -TemplateId $agreement.TemplateId -AgreementType MicrosoftCloudAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec' -ContactEmail 'someone@example.com' -ContactFirstName 'Tania' -ContactLastName 'Carr'
    ```  

## <a name="rest"></a>休息

顧客が Microsoft Cloud Agreement に同意したことを確認または再確認するには、次の手順を参照してください。

### <a name="rest-request"></a>REST 要求

1. Microsoft Cloud 契約のアグリーメントメタデータを取得します。 詳細については、「 [Microsoft Cloud agreement のアグリーメントメタデータの取得](get-agreement-metadata.md)」を参照してください。 Microsoft Cloud Agreement の**templateId**を取得するには、この手順が必要です。
2. 新しいリソースを作成して、顧客が Microsoft Cloud 契約に同意したことを確認します。 詳細については、「 [Microsoft Cloud agreement のアグリーメントメタデータの取得](get-agreement-metadata.md)」を参照してください。

新しい**アグリーメント**リソースを作成して、顧客が Microsoft Cloud 契約に同意したことを確認するには、次のようにします。

#### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを使用して、確認する顧客を指定します。

| 名前               | 種類 | 必須 | 説明                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| 顧客-テナント id | GUID | Y        | 値は、顧客を指定できるようにする GUID 形式の**顧客テナント id**です。 |

#### <a name="request-headers"></a>要求ヘッダー

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

#### <a name="request-body"></a>要求本文

次の表では、要求本文に必要なプロパティについて説明します。

| 名前      | 種類   | 説明                                                                                  |  
|-----------|--------|----------------------------------------------------------------------------------------------|  
| 契約 | オブジェクト | Microsoft Cloud 契約に対する顧客の同意を確認するためにパートナーによって提供される詳細。 |  

#### <a name="agreement"></a>契約

次の表では、**アグリーメント**リソースを作成するために必要な最小限のフィールドについて説明します。

| プロパティ       | 種類   | 説明                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Contact](./utility-resources.md#contact) | Microsoft Cloud 契約に同意したお客様の組織のユーザーに関する情報: **firstName**、 **lastName**、 **email** 、 **phoneNumber** (省略可能) |
| dateAgreed     | UTC 日時形式の文字列 |顧客がアグリーメントに同意した日付。 |
| templateId     |string | 顧客が受け入れるアグリーメントの種類を表す一意の識別子。 Microsoft Cloud Agreement のアグリーメントメタデータを取得することによって Microsoft Cloud アグリーメントの**templateId**を取得できます。 詳細については、「 [Microsoft Cloud agreement のアグリーメントメタデータの取得](get-agreement-metadata.md)」を参照してください。 |
| type           |AgreementType 列挙型 | 顧客が受け入れる契約の種類。 現在、唯一サポートされている値は "Microsoft Cloudagreement" です。 |
  
#### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
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
    "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCloudAgreement"
}
```

### <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは**アグリーメント**リソースを返します。

#### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

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
    "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCloudAgreement"
}
```

---
