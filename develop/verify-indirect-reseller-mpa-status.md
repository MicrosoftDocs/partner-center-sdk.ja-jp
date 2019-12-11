---
title: 間接リセラーの Microsoft パートナーアグリーメント署名の状態を確認する
description: AgreementStatus API を使用して、間接リセラーが Microsoft パートナー契約に署名したかどうかを確認できます。
ms.date: 10/30/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 14a66334793bfe6a1b87f0976a4084e76c331b65
ms.sourcegitcommit: 7e5e3590931010eb0e0fef3e7f6d5d7d084a69ba
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74995179"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>間接リセラーの Microsoft パートナーアグリーメント署名の状態を確認する

適用対象:

* パートナー センター
* 米国政府機関向け Microsoft Cloud のパートナー センター

間接リセラーが Microsoft Partner Network (MPN) ID またはクラウドソリューションプロバイダー (CSP) テナント ID (Microsoft ID) を使用して Microsoft パートナー契約に署名しているかどうかを確認できます。 これらの識別子のいずれかを使用して、 **AgreementStatus** API を使用して Microsoft パートナーアグリーメント署名の状態を確認できます。

## <a name="prerequisites"></a>前提条件

* 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。
* 間接リセラーの MPN ID または CSP テナント ID (Microsoft ID)。 *これら2つの識別子のいずれかを使用する必要があります。*

## <a name="c"></a>C\#

間接リセラーの Microsoft パートナー契約署名の状態を取得するには、次のようにします。

 1. **Iaggregatepartner.customers**コレクションを使用して、 **AgreementSignatureStatus**プロパティを呼び出します。 
 2. [**Get ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get)または[**GetAsync ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync)メソッドを呼び出します。

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- サンプル: **[コンソールテストアプリ](console-test-app.md)**
- プロジェクト: **Partnerセンター sdk. 特長サンプル**
- クラス: **GetAgreementSignatureStatus.cs**

## <a name="rest"></a>REST

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI |
| ------ | ----------- |
| **GET** | *[{baseURL}](partner-center-rest-urls.md)* /V1/compliance/{ProgramName}/agreementstatus? mpnid = {mpnid} & tenantid = {tenantid} |

##### <a name="uri-parameters"></a>URI パラメーター

パートナーを識別するには、次の2つのクエリパラメーターのいずれかを指定する必要があります。 これら2つのクエリパラメーターのいずれかを指定しない場合は、 **400 (Bad request)** エラーが発生します。

| 名前 | タスクバーの検索ボックスに | 必須かどうか | 説明 |
| ---- | ---- | -------- | ----------- |
| **MpnId** | 整数 | 必須ではない | 間接リセラーを識別する Microsoft Partner Network ID。 |
| **TenantId** | GUID | 必須ではない | 間接リセラーの CSP アカウントを識別する Microsoft ID。 |

#### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](https://docs.microsoft.com/partner-center/develop/headers)」を参照してください。

#### <a name="request-examples"></a>要求の例

##### <a name="request-using-mpn-id"></a>MPN ID を使用した要求

次の要求例では、間接リセラーの Microsoft Partner Network ID を使用して、間接リセラーの Microsoft パートナーアグリーメント署名の状態を取得します。

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

##### <a name="request-using-csp-tenant-id"></a>CSP テナント ID を使用した要求

次の要求例では、間接リセラーの CSP テナント ID (Microsoft ID) を使用して、間接リセラーの Microsoft パートナーアグリーメント署名の状態を取得します。

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="rest-response"></a>REST 応答

#### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターの REST エラーコード](https://docs.microsoft.com/partner-center/develop/error-codes)」を参照してください。

#### <a name="response-example-success"></a>応答の例 (成功)

次の応答例では、間接リセラーが Microsoft パートナーアグリーメントに署名しているかどうかを正常に返します。

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

#### <a name="response-examples-failure"></a>応答の例 (失敗)

間接リセラーの Microsoft パートナーアグリーメントの署名の状態を返すことができない場合、次の例のような応答が返されることがあります。

##### <a name="non-guid-formatted-csp-tenant-id"></a>GUID 形式以外の CSP テナント ID

API に渡された CSP テナント ID が GUID ではない場合、次の応答の例が返されます。

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

##### <a name="non-numeric-mpn-id"></a>数値以外の MPN ID

次の応答例は、API に渡された MPN ID が非数値である場合に返されます。

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

##### <a name="no-mpn-id-or-csp-tenant-id"></a>MPN ID または CSP テナント ID がありません

API に MPN ID または CSP テナント ID を渡さなかった場合に返される応答の例を次に示します。 2種類の ID のいずれかを API に渡す必要があります。

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

##### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>MPN ID と CSP テナント ID の両方が渡されました

MPN ID と CSP テナント ID の両方を API に渡すと、次の応答の例が返されます。 API には、2つの識別子の型の*うち1つだけ*を渡す必要があります。

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
