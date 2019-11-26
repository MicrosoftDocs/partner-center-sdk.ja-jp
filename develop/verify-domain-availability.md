---
title: Verify domain availability
description: How to determine if a domain is available for use.
ms.assetid: 9ECF8241-3672-441D-B34D-83F7C23138B3
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 79f68fe92f22a4e5a6793f97b55da16adee19b5a
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486242"
---
# <a name="verify-domain-availability"></a>Verify domain availability


**Applies To**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

How to determine if a domain is available for use.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A domain (e.g. "contoso.onmicrosoft.com").

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


To verify if a domain is available, first call [**IAggregatePartner.Domains**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.domains) to obtain an interface to domain operations. Then call the [**ByDomain**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) method with the domain to check. This retrieves an interface to the operations available for a specific domain. Finally, call the [**Exists**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) method to see if the domain already exists.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";  

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CheckDomainAvailability.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>Request


**Request syntax**

| メソッド   | 要求 URI                                                              |
|----------|--------------------------------------------------------------------------|
| **HEAD** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1 |

 

**URI parameter**

Use the following query parameter to verify domain availability.

| 名前       | タスクバーの検索ボックスに       | 必須かどうか | 説明                                   |
|------------|------------|----------|-----------------------------------------------|
| **domain** | **string** | Y        | A string that identifies the domain to check. |

 

**Request headers**

- See [Partner Center REST headers](headers.md) for more information.

**Request body**

なし

**Request example**

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>Response


If the domain exists it is not available for use and a response status code 200 OK is returned. If the domain is not found it is available for use and a response status code 404 Not Found is returned.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example for when the domain is already in use**

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

**Response example for when the domain is available**

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```

 

 




