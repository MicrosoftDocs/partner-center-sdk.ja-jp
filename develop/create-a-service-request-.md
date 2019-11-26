---
title: Create a service request
description: How to create a partner center service request.
ms.assetid: 16DA9836-7052-4103-82D4-933E5EEB7E71
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7dcac9a9938f9d197d3ece0d7b777e7efc40274b
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489322"
---
# <a name="create-a-service-request"></a>Create a service request

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

How to create a partner center service request.

## <a name="prerequisites"></a>前提条件

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
- A support topic ID. If you do not have a support topic ID, see [Get service request support topics](get-service-request-support-topics--pending-.md).

## <a name="c"></a>C\#

To create a service request:

1. Create and populate a [**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object with the title, description, severity, and support topic id. To add additional information, the [**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object supports an optional collection of [**Notes**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.notes), but does not support links to files for uploading.
2. Once the object is created, call the [**IAggregatePartner.ServiceRequests.Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.ipartnerservicerequestcollection.create) method, passing it the newly created ServiceRequest object and a string containing the locale of the organization creating the service request (the agent locale).

### <a name="c-example"></a>C\# example

``` csharp
// IAggregatePartner partnerOperations;
// string supportTopicId;

ServiceRequest serviceRequestToCreate = new ServiceRequest()
{
    Title = "TrialSR",
    Description = "Ignore this SR",
    Severity = ServiceRequestSeverity.Critical,
    SupportTopicId = supportTopicId
};

ServiceRequest serviceRequest = partnerOperations.ServiceRequests.Create(serviceRequestToCreate, "en-US");
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CreatePartnerServiceRequest.cs

## <a name="rest-request"></a>REST request

### <a name="request-syntax"></a>要求の構文

| メソッド   | 要求 URI                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/servicerequests/{agent-locale} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

Use the following URI parameter to identify the agent locale.

| 名前             | タスクバーの検索ボックスに       | 必須かどうか | 説明                                                  |
|------------------|------------|----------|--------------------------------------------------------------|
| **agent-locale** | **string** | Y        | The locale of the organization creating the service request. |

### <a name="request-headers"></a>要求ヘッダー

See [Partner Center REST headers](headers.md) for more information.

### <a name="request-body"></a>要求本文

This table describes the required and optional properties in the request body.

| 名前             | タスクバーの検索ボックスに                                                                        | 必須かどうか | 説明                                                                          |
|------------------|-----------------------------------------------------------------------------|----------|--------------------------------------------------------------------------------------|
| Title (タイトル)            | string                                                                      | Y        | The service request title.                                                           |
| 説明      | string                                                                      | Y        | The description.                                                                     |
| 重大度         | string                                                                      | Y        | The severity: "unknown", "critical", "moderate", or "minimal".                       |
| SupportTopicId   | string                                                                      | Y        | The id of the support topic.                                                         |
| SupportTopicName | string                                                                      | N        | The name of the support topic.                                                       |
| Id               | string                                                                      | N        | The id of the service request.                                                       |
| 状況           | string                                                                      | N        | The status of the service request: "none", "open", "closed", or "attention\_needed". |
| 組織     | [ServiceRequestOrganization](service-request-resources.md#servicerequestorganization) | N        | Organization for which the service request is created.                               |
| PrimaryContact   | [ServiceRequestContact](service-request-resources.md#servicerequestcontact)           | N        | Primary Contact on the service request.                                              |
| LastUpdatedBy    | [ServiceRequestContact](service-request-resources.md#servicerequestcontact)           | N        | "Last Updated By" contact for changes to the service request.                        |
| ProductName      | string                                                                      | N        | The name of the product that corresponds to the service request.                     |
| ProductId        | string                                                                      | N        | The id of the product.                                                               |
| CreatedDate      | date                                                                        | N        | The date of the service request's creation.                                          |
| LastModifiedDate | date                                                                        | N        | The date that the service request was last modified.                                 |
| LastClosedDate   | date                                                                        | N        | The date that the service request was last closed.                                   |
| FileLinks        | array of [FileInfo](utility-resources.md#fileinfo) resources               | N        | The collection of File Links that pertain to the service request.                    |
| NewNote          | [ServiceRequestNote](service-request-resources.md#servicerequestnote)                 | N        | A note can be added to an existing service request.                                  |
| 注意            | array of [ServiceRequestNotes](service-request-resources.md#servicerequestnote)       | N        | A collection of notes added to the service request.                                  |
| CountryCode      | string                                                                      | N        | The country corresponding to the service request.                                    |
| 属性       | オブジェクト                                                                      | N        | Contains "ObjectType": "ServiceRequest".                                             |

This table describes the required properties in the request body.

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/servicerequests/en-US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 55f86bfb-d3bb-4fe4-9f01-2fdaef11a81f
MS-CorrelationId: ae43859b-591d-47ea-9fd1-028b4c799118
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 474
Expect: 100-continue

{
    "Id": null,
    "Title": "TrialSR",
    "Description": "Ignore this SR",
    "Severity": "critical",
    "SupportTopicId": "32444671",
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": null,
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a>REST response

If successful, this method returns the **Service Request** resource properties in the response body.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 201 Created
Content-Length: 721
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae43859b-591d-47ea-9fd1-028b4c799118
MS-RequestId: 55f86bfb-d3bb-4fe4-9f01-2fdaef11a81f
MS-CV: vB9EuWs/ukaxQmuV.0
MS-ServerId: 101112616
Date: Thu, 22 Dec 2016 20:31:14 GMT

 {
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "id": "616122292874576",
    "status": "none",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1",
        "phoneNumber": "2398391056"
    },
    "primaryContact": {
        "organization": {
            "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "name": "TEST_TEST_BugBash1",
            "phoneNumber": "2398391056"
        },
        "contactId": "bb4ebcf5-d84c-4b35-8469-f4cfa4ac909e",
        "lastName": "Account",
        "email": "admin@testtestbugbash1.onmicrosoft.com",
        "phoneNumber": "2066017143"
    },
    "createdDate": "0001-01-01T00:00:00",
    "lastModifiedDate": "0001-01-01T00:00:00",
    "lastClosedDate": "0001-01-01T00:00:00",
    "countryCode": "US",
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```