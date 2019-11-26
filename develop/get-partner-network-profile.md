---
title: プロファイルの取得 Microsoft Partner Network
description: パートナーの MPN プロファイルを表すオブジェクトを取得します。
ms.assetid: 6DC85E2F-0AC8-4166-883B-CCFD19044FC1
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7dbd49b70ff3d7c329bc4c61055a66a2476b7e62
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74490312"
---
# <a name="get-microsoft-partner-network-profile"></a>プロファイルの取得 Microsoft Partner Network

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーの MPN プロファイルを表すオブジェクトを取得します。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="span-idexamplesspan-idexamplesspan-idexamplesexamples"></a><span id="Examples"/><span id="examples"><span id="EXAMPLES"/>の例

### <a name="c"></a>C#

パートナーネットワークプロファイルを取得するには、 **iaggregatepartner.customers**コレクションを使用して**mpnprofile**プロパティを呼び出します。 最後に、 [**Get ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get)メソッドまたは[**GetAsync ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync)メソッドを呼び出します。

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**:P artによって、GetMPNProfile.cs サンプル**クラス**:

### <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

パートナーネットワークプロファイルを取得するには、 **iaggregatepartner.customers**関数を使用し、 **Getmpnprofile**関数を呼び出します。 最後に、 **get ()** 関数を呼び出します。

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

### <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

パートナーネットワークプロファイルを取得するには、 [**Get PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md)コマンドを実行します。

```powershell
Get-PartnerMpnProfile
```

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求

**要求の構文**

| メソッド  | 要求 URI                                                          |
|---------|----------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1 |

 
**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答

成功した場合、このメソッドは応答本文で**Mpnprofile**オブジェクトを返します。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
Date: Mon, 21 Mar 2016 05:51:29 GMT

{
    "mpnId":"<mpnID>",
    "profileType":"MpnProfile",
    "links":{
        "self":{
            "uri":"/profiles/mpn",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"MpnProfile"
    }
}
```