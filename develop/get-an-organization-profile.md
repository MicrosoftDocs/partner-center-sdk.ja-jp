---
title: 組織のプロファイルを取得する
description: パートナーの組織プロファイルを表すオブジェクトを取得します。
ms.assetid: 2AA159F1-CC84-4367-A2AF-DFA4C8B0E673
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ecfa4c88244b65bbc70af29c322b877759140ee0
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485732"
---
# <a name="get-an-organization-profile"></a>組織のプロファイルを取得する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーの組織プロファイルを表すオブジェクトを取得します。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="span-idexamplesspan-idexamplesspan-idexamplesexamples"></a><span id="Examples"/><span id="examples"><span id="EXAMPLES"/>の例

### <a name="c"></a>C#

組織のプロファイルを取得するには、 **iaggregatepartner.customers**コレクションを使用して、[組織の**プロファイル**] プロパティを呼び出します。 最後に、 [**Get ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get)メソッドまたは[**GetAsync ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync)メソッドを呼び出します。

```csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: partnerセンター sdk. のサンプル**クラス**: GetOrganizationProfile.cs

### <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

組織のプロファイルを取得するには、 **iaggregatepartner.customers**関数を使用し、 **getprofiles profile**関数を呼び出します。 最後に、 **get ()** 関数を呼び出します。

```java
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.getProfiles().getOrganizationProfile().get();
```

### <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

組織のプロファイルを取得するには、 [**Get Partnerのプロファイル**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md)コマンドを実行します。 

```powershell
Get-PartnerOrganizationProfile
```

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求

**要求の構文**

| メソッド  | 要求 URI                                                                   |
|---------|-------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1 |

**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答

成功した場合、このメソッドは、応答本文に**組織のプロファイル**オブジェクトを返します。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 648
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
Date: Tue, 22 Mar 2016 17:11:06 GMT

{
    "id":<id>,
    "companyName":"TEST_TEST_BugBash1",
    "defaultAddress":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"Two Microsoft Way",
        "addressLine2":"",
        "postalCode":"98052",
        "firstName":"Test",
        "lastName":"Account",
        "phoneNumber":""
    },
    "tenantId":<tenantID>,
    "domain":"testtestbugbash1.onmicrosoft.com",
    "email":"test-partner@microsoft.com",
    "language":"es",
    "culture":"es-US",
    "profileType":"OrganizationProfile",
    "links":{
        "self":{
            "uri":"/profiles/organization",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"OrganizationProfile"
    }
}
```