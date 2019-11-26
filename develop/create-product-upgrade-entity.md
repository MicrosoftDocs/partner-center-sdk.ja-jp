---
title: 顧客の製品アップグレードエンティティを作成する
description: Productupgrade によるリソースを使用して、製品のアップグレードエンティティを作成し、特定の製品ファミリに顧客をアップグレードすることができます。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: de3382ce6815279528d599f5f039e44358593875
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489582"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a>顧客の製品アップグレードエンティティを作成する

適用対象:

- パートナー センター

製品アップグレードエンティティを作成して、 **productupgrade**のリソースを使用して、顧客を特定の製品ファミリ (たとえば、Azure プラン) にアップグレードすることができます。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報を使用した認証がサポートされます。 パートナーセンター Api でアプリとユーザー認証を使用する場合は、[セキュリティで保護されたアプリモデル](enable-secure-app-model.md)に従います。
- 顧客識別子。
- 顧客のアップグレード先となる製品ファミリ。

## <a name="c"></a>C\#

顧客を Azure プランにアップグレードするには:

1. **Product・アップグレード Esrequest**オブジェクトを作成し、製品ファミリとして顧客識別子と "Azure" を指定します。
2. **Iaggregatepartner.customers**コレクションを使用します。
3. **Create**メソッドを呼び出し、 **productの要求**オブジェクトを渡します。これにより、**場所ヘッダー**文字列が返されます。
4. [アップグレードの状態を照会](get-product-upgrade-status.md)するために使用できる場所ヘッダー文字列から**アップグレード id**を抽出します。

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "Azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

var productUpgradeLocationHeader = partnerOperations.ProductUpgrades.Create(productUpgradeRequest);

var upgradeId = Regex.Split(productUpgradeLocationHeader, "/")[1];

```

## <a name="rest"></a>休息

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求の構文

| メソッド   | 要求 URI                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **投稿** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1 |

#### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md)」を参照してください。

#### <a name="request-body"></a>要求本文

要求本文には、 [Productアップグレード](product-upgrade-resources.md#productupgraderequest)のためのリソースが含まれている必要があります。

#### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
  "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
  "productFamily": "Azure"
}
```

### <a name="rest-response"></a>REST 応答

成功した場合、応答には、製品のアップグレード状態を取得するために使用できる URI を含む**Location**ヘッダーが含まれます。 他の関連する REST Api で使用するために、この URI を保存します。

#### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

#### <a name="response-example"></a>応答の例

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: productUpgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2019 20:35:35 GMT
```
