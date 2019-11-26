---
title: Verify an indirect reseller's Microsoft Partner Agreement signing status
description: You can use the AgreementStatus API to verify whether an indirect reseller has signed the Microsoft Partner Agreement.
ms.date: 10/30/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2b7785aa3b419ff5160031fb338e78f7130d5b9f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487712"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>Verify an indirect reseller's Microsoft Partner Agreement signing status

適用対象:

* パートナー センター
* 米国政府機関向け Microsoft Cloud のパートナー センター

You can verify whether an indirect reseller has signed the Microsoft Partner Agreement using their Microsoft Partner Network (MPN) ID or Cloud Solution Provider (CSP) tenant ID (Microsoft ID). You can use one of these identifiers to check the Microsoft Partner Agreement signing status using the **AgreementStatus** API.

## <a name="prerequisites"></a>前提条件

* Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
* The MPN ID or the CSP tenant ID (Microsoft ID) of the indirect reseller. *You must use one of these two identifiers.*

## <a name="rest"></a>REST

### <a name="rest-request"></a>REST request

#### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI |
| ------ | ----------- |
| **GET** | *[{baseURL}](partner-center-rest-urls.md)* /v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId} |

##### <a name="uri-parameters"></a>URI パラメーター

You must provide one of the following two query parameters to identify the partner. If you don't provide one of these two query parameters, you will receive a **400 (Bad request)** error.

| 名前 | タスクバーの検索ボックスに | 必須かどうか | 説明 |
| ---- | ---- | -------- | ----------- |
| **MpnId** | 整数 | 必須ではない | A Microsoft Partner Network ID that identifies the indirect reseller. |
| **TenantId** | GUID | 必須ではない | A Microsoft ID that identifies the CSP account of the indirect reseller. |

#### <a name="request-headers"></a>要求ヘッダー

For more information, see [Partner Center REST headers](https://docs.microsoft.com/en-us/partner-center/develop/headers).

#### <a name="request-examples"></a>要求の例

##### <a name="request-using-mpn-id"></a>Request using MPN ID

The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's Microsoft Partner Network ID.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

##### <a name="request-using-csp-tenant-id"></a>Request using CSP tenant ID

The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's CSP tenant ID (Microsoft ID).

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="rest-response"></a>REST response

#### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](https://docs.microsoft.com/en-us/partner-center/develop/error-codes).

#### <a name="response-example-success"></a>Response example (success)

The following example response successfully returns whether the indirect reseller has signed the Microsoft Partner Agreement.

```http
HTTP/1.1 200 OK
Content-Length: 29
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: jn3r+1wpE06nCt/0.0
MS-ServerId: 0000005B
Date: Tue, 15 Oct 2019 12:44:34 GMT
Connection: close
{
    "isAgreementSigned": true
}
```

#### <a name="response-examples-failure"></a>Response examples (failure)

You may receive responses similar to the following examples when the signing status of the indirect reseller's Microsoft Partner Agreement can't be returned.

##### <a name="non-guid-formatted-csp-tenant-id"></a>Non-GUID formatted CSP tenant ID

The following example response is returned when the CSP tenant ID that you passed to the API is not a GUID.

```http
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: rbuZl5lbAkyq8WGK.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 08:55:23 GMT
Connection: close
{
    "code": 2000,
    "description": "Tenant Id must be a GUID.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

##### <a name="non-numeric-mpn-id"></a>Non-numeric MPN ID

The following example response is returned when the MPN ID that you passed to the API is non-numeric.

```http
HTTP/1.1 400 Bad Request
Content-Length: 103
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: cP5JiS4sv0GJxlJ9.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 08:58:45 GMT
Connection: close
{
    "code": 2000,
    "description": "MPN Id must be numeric.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

##### <a name="no-mpn-id-or-csp-tenant-id"></a>No MPN ID or CSP tenant ID

The following example response is returned when you haven't passed an MPN ID or CSP tenant ID to the API. You must pass one of the two ID types to the API.

```http
HTTP/1.1 400 Bad Request
Content-Length: 114
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: hEV736v4qk6joDMR.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 09:00:30 GMT
Connection: close
{
    "code": 2001,
    "description": "Both MPN Id and Tenant Id cannot be empty.",
    "data": [],
    "source": "ComplianceController"
}
```

##### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>Both MPN ID and CSP tenant ID passed

The following example response is returned when you pass both the MPN ID and CSP tenant ID to the API. You must pass *only one* of the two identifier types to the API.

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2000,
    "description": "Both MPN Id and Tenant Id should not be passed.",
    "data": [],
    "source": "ComplianceController"
}
```
