---
title: Azure プランへのアップグレードについてお客様の資格を確認する
description: ProductProductUpgradesEligibility リソースを使用して、顧客が Microsoft Azure (MS AZR-0145P) サブスクリプションから Azure プランにアップグレードできるかどうかを判断することができます。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: b94aa50364ef770a843624d397240e35eaa8cecf
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415937"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a>Azure プランへのアップグレードについてお客様の資格を確認する

適用対象

- Partner Center

[**Productupgraderequest**](product-upgrade-resources.md#productupgraderequest)リソースを使用して、顧客が Microsoft Azure (ProductUpgradesEligibility 5p) サブスクリプションから Azure プランにアップグレードできるかどうかを確認できます。この方法では、お客様の製品のアップグレード資格を持つ[**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility)リソースが返されます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証がサポートされます。 パートナーセンター Api でアプリとユーザー認証を使用する場合は、[セキュリティで保護されたアプリモデル](enable-secure-app-model.md)に従います。
- 顧客識別子。
- 製品ファミリ。

## <a name="c"></a>C\#

顧客が Azure プランにアップグレードする資格があるかどうかを確認するには、次のようにします。

1. **Product・アップグレード Esrequest**オブジェクトを作成し、製品ファミリとして顧客識別子と "Azure" を指定します。
2. **Iaggregatepartner.customers**コレクションを使用します。
3. **CheckEligibility**メソッドを呼び出し、 **Product esrequest**オブジェクトを渡します。これにより、 **ProductUpgradesEligibility**オブジェクトが返されます。

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesEligibility productUpgradeEligibility = partnerOperations.ProductUpgrades.CheckEligibility(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest"></a>REST

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求の構文

| メソッド   | 要求 URI                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1 |

#### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

#### <a name="request-body"></a>[要求本文]

要求本文には、 [**Productアップグレード**](product-upgrade-resources.md#productupgraderequest)のためのリソースが含まれている必要があります。

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
    {
        "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
        "productFamily": "azure"
    }
    "Attributes": {
    "ObjectType": "ProductUpgradeRequest"
    }
}
```

### <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは本文で[**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility)リソースを返します。

#### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

#### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
