---
title: 間接リセラーの Microsoft Partner Agreement の署名状態を確認する
description: AgreementStatus API を使用して、間接リセラーが Microsoft パートナー契約に署名したかどうかを確認できます。
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4836a5e0646e1f00807966d3d8d332c026276c61
ms.sourcegitcommit: 68a5497a7350e135358aeb7f2a54c75707f922c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87261941"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>間接リセラーの Microsoft Partner Agreement の署名状態を確認する

**適用対象:**

- パートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

間接リセラーが Microsoft Partner Network (MPN) ID またはクラウド ソリューション プロバイダー (CSP) テナント ID (Microsoft ID) を使用して Microsoft パートナー契約に署名しているかどうかを確認できます。 これらの識別子のいずれかを使用して、**AgreementStatus** API を使って、Microsoft Partner Agreement の署名状態を確認できます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 間接リセラーの MPN ID または CSP テナント ID (Microsoft ID)。 "*これら 2 つの識別子のいずれかを使用する必要があります。* "

## <a name="c"></a>C\#

間接リセラーの Microsoft Partner Agreement の署名状態を確認するには、次の手順に従います。

1. **IAggregatePartner.Compliance** コレクションを使用して、**AgreementSignatureStatus** プロパティを呼び出します。

2. [**Get()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) または [**GetAsync()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) メソッドを呼び出します。

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- サンプル: **[コンソール テスト アプリ](console-test-app.md)**
- プロジェクト:**PartnerCenterSDK.FeaturesSamples**
- Class:**GetAgreementSignatureStatus.cs**

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法 | 要求 URI |
| ------ | ----------- |
| **GET** | *[{baseURL}](partner-center-rest-urls.md)* /v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId} |

#### <a name="uri-parameters"></a>URI パラメーター

パートナーを識別するには、次の 2 つのクエリ パラメーターのいずれかを指定する必要があります。 これら 2 つのクエリ パラメーターのいずれかを指定しなかった場合、**400 (無効な要求)** エラーが発生します。

| 名前 | 種類 | 必須 | 説明 |
| ---- | ---- | -------- | ----------- |
| **MpnId** | int | いいえ | 間接リセラーを識別する Microsoft Partner Network ID。 |
| **TenantId** | GUID | いいえ | 間接リセラーの CSP アカウントを識別する Microsoft ID。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](https://docs.microsoft.com/partner-center/develop/headers)」を参照してください。

### <a name="request-examples"></a>要求の例

#### <a name="request-using-mpn-id"></a>MPN ID を使用した要求

次の要求例では、間接リセラーの Microsoft Partner Network ID を使用して、間接リセラーの Microsoft Partner Agreement の署名状態を取得します。

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a>CSP テナント ID を使用した要求

次の要求例では、間接リセラーの CSP テナント ID (Microsoft ID) を使用して、間接リセラーの Microsoft Partner Agreement の署名状態を取得します。

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 応答

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](https://docs.microsoft.com/partner-center/develop/error-codes)に関する記事を参照してください。

### <a name="response-example-success"></a>応答の例 (成功)

次の応答例では、間接リセラーが Microsoft パートナー契約に署名しているかどうかが正常に返されます。

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

### <a name="response-examples-failure"></a>応答の例 (失敗)

間接リセラーの Microsoft パートナー契約の署名状態を返すことができない場合、次の例のような応答が返されることがあります。

#### <a name="non-guid-formatted-csp-tenant-id"></a>GUID ではないフォーマット済み CSP テナント ID

API に渡された CSP テナント ID が GUID ではない場合、次の例の応答が返されます。

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

#### <a name="non-numeric-mpn-id"></a>数値以外の MPN ID

API に渡した MPN ID が数値ではない場合、次の応答の例が返されます。

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

#### <a name="no-mpn-id-or-csp-tenant-id"></a>MPN ID または CSP テナント ID がない場合

MPN ID または CSP テナント ID を API に渡していない場合、次の応答の例が返されます。 2 つのいずれかの種類の ID を API に渡す必要があります。

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>MPN ID と CSP テナント ID の両方を渡した場合

MPN ID と CSP テナント ID の両方を API に渡した場合、次の応答の例が返されます。 2 つの種類の ID の "*いずれか 1 つのみ*" を API に渡す必要があります。

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

#### <a name="csp-indirect-reseller-mpn-id-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>CSP Indirect Reseller の MPN ID が無効であるか、Partner Membership Center からパートナー センターに移行されていない

次の応答の例は、渡された間接リセラー MPN ID が無効であるか、Partner Membership Center からパートナー センターに移行されていない場合に返されます。 [詳細情報](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2200,
    "description": "MPN Id 123456 is either invalid or not yet migrated to Partner Center. Please advise your reseller to migrate the reseller MPN ID to Partner Center to continue with this order.",
    "data": [
        "https://partner.microsoft.com/en-us/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>CSP Indirect Provider の地域と CSP Indirect Reseller の地域が一致しない

次の応答の例は、間接リセラー MPN ID の地域が間接プロバイダーの地域と一致しない場合に返されます。 [CSP の地域の詳細](https://docs.microsoft.com/partner-center/regional-authorization-overview)をご確認ください。

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
    "code": 2201,
    "description": "The CSP region of the MPN ID 1234567 doesn’t match the CSP region from where you are placing the order. Provide the MPN ID for the CSP region where you are placing the order.",
    "data": [
        "https://docs.microsoft.com/en-us/partner-center/regional-authorization-overview" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>CSP 間接リセラー アカウントはパートナー センターに存在するが、MPA に署名されていない

次の応答の例は、パートナー センターの CSP Indirect Reseller アカウントで MPA に署名されていない場合に返されます。 [詳細情報](https://partner.microsoft.com/resources/detail/verify-mpa-acceptance-status-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2203,
    "description": "MPN Id 123456 has not signed Microsoft Partner Agreement (MPA) for the CSP region where the order is being placed. Please advise your reseller to sign MPA to continue with the order.",
    "data": [
        "https://partner.microsoft.com/en-gb/resources/detail/verify-mpa-acceptance-status-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>指定された MPN ID に関連付けられた CSP Indirect Reseller アカウントがない

次の応答の例は、要求で渡された MPN ID はパートナー センターで認識されるが、指定された MPN ID に関連付けられた CSP 登録がない場合に返されます。 [詳細情報](https://partner.microsoft.com/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2204,
    "description": "MPN Id 123456 is not associated with a CSP Indirect Reseller account in Partner Center. Please advise your reseller to enroll into the CSP program as an indirect reseller in Partner Center.",
    "data": [
        "https://partner.microsoft.com/en-us/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a>無効なテナント ID

次の応答例は、要求で渡されたテナント ID に関連付けられたアカウントがパートナー センターで見つからない場合に返されます。

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2205,
    "description": "Partner Center doesn't find any account associated to the Tenant ID 12345678-ACBD-1234-ABCD-123456789ABC",
    "data": [],
    "source": "PartnerFD"
}
```

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>指定されたテナント ID の MPA が見つからない

次の応答例は、指定されたテナント ID を持つ MPA 署名がパートナー センターで見つからない場合に返されます。

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2206,
    "description": "Parnter Center Account associated to Tenant Id 12345678-ACBD-1234-ABCD-123456789ABC hasn't signed the agreement",
    "data": [],
    "source": "PartnerFD"
}
```
