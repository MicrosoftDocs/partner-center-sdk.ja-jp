---
title: Microsoft Partner Network プロファイルを取得する
description: パートナーの MPN プロファイルを表すオブジェクトを取得します。
ms.assetid: 6DC85E2F-0AC8-4166-883B-CCFD19044FC1
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: b8b4d757bb881cac5f261e15f34eb49822f3af30
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157304"
---
# <a name="get-microsoft-partner-network-profile"></a>Microsoft Partner Network プロファイルを取得する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーの MPN プロファイルを表すオブジェクトを取得します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="c"></a>C\#

パートナーネットワークプロファイルを取得するには、 **iaggregatepartner.customers**コレクションを使用して**mpnprofile**プロパティを呼び出します。 最後に、 [**Get ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get)メソッドまたは[**GetAsync ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync)メソッドを呼び出します。

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**:P artによって、GetMPNProfile.cs サンプル**クラス**:

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

パートナーネットワークプロファイルを取得するには、 **iaggregatepartner.customers**関数を使用し、 **Getmpnprofile**関数を呼び出します。 最後に、 **get ()** 関数を呼び出します。

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

パートナーネットワークプロファイルを取得するには、 [**Get PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md)コマンドを実行します。

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                          |
|---------|----------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で**Mpnprofile**オブジェクトを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

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
