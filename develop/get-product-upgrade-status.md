---
title: 顧客の製品のアップグレード状態を取得する
description: ProductUpgradeRequest リソースを使用して、顧客の製品のアップグレードの状態を、新しい製品ファミリに (たとえば、Azure プランの Microsoft Azure (MS AZR-5P) サブスクリプションから) 確認できます。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c99b70f4046a0018d43f395fe7539f608cecf11f
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416701"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a>顧客の製品のアップグレード状態を取得する

適用対象

- Partner Center

[**Productupgrade**](product-upgrade-resources.md#productupgraderequest)のリソースを使用して、新しい製品ファミリへのアップグレードの状態を取得できます。 このリソースは、Microsoft Azure (MS AZR-0145P) サブスクリプションから Azure プランに顧客をアップグレードするときに適用されます。 要求が成功すると、 [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility)リソースが返されます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証がサポートされます。 パートナーセンター Api でアプリとユーザー認証を使用する場合は、[セキュリティで保護されたアプリモデル](enable-secure-app-model.md)に従います。
- 顧客識別子。
- 製品ファミリ。
- アップグレード要求のアップグレード id。

## <a name="c"></a>C\#

顧客が Azure プランにアップグレードする資格があるかどうかを確認するには、次のようにします。

1. **Product・アップグレード Esrequest**オブジェクトを作成し、製品ファミリとして顧客識別子と "Azure" を指定します。
2. **Iaggregatepartner.customers**コレクションを使用します。
2. **ById**メソッドを呼び出し、**アップグレード id**を渡します。
3. **Checkstatus**メソッドを呼び出し、 **Productupgradesrequest**オブジェクトを渡します。これにより、 **productupgradestatus**オブジェクトが返されます。

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```
```

## REST

### REST request

#### Request syntax

| Method   | Request URI |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1 |

#### URI parameter

Use the following query parameter to specify the customer for whom you're getting a product upgrade status.

| Name               | Type | Required | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **upgrade-id** | GUID | Yes | The value is a GUID-formatted upgrade identifier. You can use this identifier to specify an upgrade to track. |

#### Request headers

For more information, see [Partner Center REST headers](headers.md).

#### Request body

The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.

#### Request example

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
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
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```
