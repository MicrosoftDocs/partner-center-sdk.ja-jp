---
title: Confirm customer acceptance of Microsoft Cloud Agreement
description: How to confirm customer acceptance of the Microsoft Cloud Agreement.
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
# <a name="confirm-customer-acceptance-of-microsoft-cloud-agreement"></a>Confirm customer acceptance of Microsoft Cloud Agreement

適用対象:

- パートナー センター

> [!NOTE]  
> The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only. 以下には適用されません。
> - 21Vianet が運営するパートナー センター
> - Microsoft Cloud ドイツのパートナー センター
> - 米国政府機関向け Microsoft Cloud のパートナー センター

How to confirm customer acceptance of the Microsoft Cloud agreement.

## <a name="prerequisites"></a>前提条件

- If you are using the Partner Center .NET SDK, version 1.9 or newer is required.
- If you are using the Partner Center Java SDK, version 1.8 or newer is required.
- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario supports app + user authentication only.
- A customer ID (customer-tenant-id).
- Date when customer accepted the Microsoft Cloud Agreement.
- Information about the user from the organization who accepted the Microsoft Cloud Agreement, including:
  - 名
  - 姓
  - メール アドレス
  - 電話番号 (オプション)


## <a name="net-version-114-or-newer"></a>.NET (version 1.14 or newer)

To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:

1. Retrieve the agreement metadata for the Microsoft Cloud Agreement. You must obtain the **templateId** of the Microsoft Cloud Agreement. For more details, see [Get agreement metadata for Microsoft Cloud Agreement](get-agreement-metadata.md).

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. Create a new **Agreement** object containing details of the confirmation.
3. Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.
4. Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.

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

A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.

## <a name="net-version-19---113"></a>.NET (version 1.9 - 1.13)

To confirm or re-confirm that a customer has accepted the Microsoft Cloud Agreement:

1. Retrieve the agreement metadata for the Microsoft Cloud Agreement. See [Get agreement metadata for Microsoft Cloud Agreement](get-agreement-metadata.md) for details. This step is required to obtain the **TemplateId** of the Microsoft Cloud Agreement.

    ```csharp
    /// IAggregatePartner partnerOperations;
    var agreements = partnerOperations.AgreementDetails.Get();

    AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
    ```

2. Create a new **Agreement** object containing details of the confirmation. Then use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's ID. Then, call the **Agreements** property, followed by calling **Create** or **CreateAsync**.

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

To confirm or re-confirm that a customer has accepted the Microsoft Cloud Agreement:

1. Retrieve the agreement metadata for the Microsoft Cloud Agreement. See [Get agreement metadata for Microsoft Cloud Agreement](get-agreement-metadata.md) for details. This step is required to obtain the **TemplateId** of the Microsoft Cloud Agreement.

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

2. Create a new **Agreement** object containing details of the confirmation. Then use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier. Then, call the **getAgreements** property, followed by calling the **create** function.

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

A complete sample can be found in the [CreateCustomerAgreement](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/src/main/java/com/microsoft/store/partnercenter/samples/agreements/CreateCustomerAgreement.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

To confirm or re-confirm that a customer has accepted the Microsoft Cloud Agreement:

1. Retrieve the agreement metadata for the Microsoft Cloud Agreement. See [Get agreement metadata for Microsoft Cloud Agreement](get-agreement-metadata.md) for details. This step is required to obtain the **TemplateId** of the Microsoft Cloud Agreement.  

    ```powershell  
    $agreement = Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
    ```  

2. Execute the [**New-PartnerCustomerAgreement**](https://docs.microsoft.com/powershell/module/partnercenter/partner-center/new-partnercustomeragreement) command  

    ```powershell  
    New-PartnerCustomerAgreement -TemplateId $agreement.TemplateId -AgreementType MicrosoftCloudAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec' -ContactEmail 'someone@example.com' -ContactFirstName 'Tania' -ContactLastName 'Carr'
    ```  

## <a name="rest"></a>REST

To confirm or re-confirm that a customer has accepted the Microsoft Cloud Agreement, see the following instructions.

### <a name="rest-request"></a>REST request

1. Retrieve the agreement metadata for the Microsoft Cloud Agreement. See [Get agreement metadata for Microsoft Cloud Agreement](get-agreement-metadata.md) for details. This step is required to obtain the **templateId** of the Microsoft Cloud Agreement.
2. Create a new resource to confirm that a customer has accepted the Microsoft Cloud Agreement. See [Get agreement metadata for Microsoft Cloud Agreement](get-agreement-metadata.md) for details.

To create a new **Agreement** resource to confirm that a customer has accepted the Microsoft Cloud Agreement:

#### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

Use the following query parameter to specify the customer you are confirming.

| 名前               | タスクバーの検索ボックスに | 必須かどうか | 説明                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | Y        | The value is a GUID formatted **customer-tenant-id** that allows you to specify a customer. |

#### <a name="request-headers"></a>要求ヘッダー

- See [Partner Center REST headers](headers.md) for more information.

#### <a name="request-body"></a>要求本文

This table describes the required properties in the request body.

| 名前      | タスクバーの検索ボックスに   | 説明                                                                                  |  
|-----------|--------|----------------------------------------------------------------------------------------------|  
| 契約 | オブジェクト | Details provided by partner to confirm customer acceptance of the Microsoft Cloud Agreement. |  

#### <a name="agreement"></a>契約

This table describes the minimum required fields to create an **Agreement** resource.

| プロパティ       | タスクバーの検索ボックスに   | 説明                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Contact](./utility-resources.md#contact) | Information about the user from the customer organization who accepted the Microsoft Cloud Agreement, including:  **firstName**, **lastName**, **email** and **phoneNumber** (optional) |
| dateAgreed     | string in UTC date time format |The date when the customer accepted the agreement. |
| templateId     |string | Unique identifier of the agreement type accepted by the customer. You can obtain the **templateId** for Microsoft Cloud Agreement by retrieving the agreement metadata for Microsoft Cloud Agreement. See [Get agreement metadata for Microsoft Cloud Agreement](get-agreement-metadata.md) for details. |
| type           |AgreementType enum | Agreement type accepted by the customer. Currently, the only supported value is "MicrosoftCloudAgreement". |
  
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

### <a name="rest-response"></a>REST response

If successful, this method returns an **Agreement** resource.

#### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

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
