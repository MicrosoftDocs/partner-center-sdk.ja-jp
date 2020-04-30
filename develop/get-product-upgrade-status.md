---
title: 顧客の製品のアップグレード状態を取得する
description: ProductUpgradeRequest リソースを使用して、顧客の製品のアップグレードの状態を、新しい製品ファミリに (たとえば、Azure プランの Microsoft Azure (MS AZR-5P) サブスクリプションから) 確認できます。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 98737e75c643cb9ca90572544173fe5000f475d9
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157274"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a>顧客の製品のアップグレード状態を取得する

**適用対象:**

- パートナー センター

[**Productupgrade**](product-upgrade-resources.md#productupgraderequest)のリソースを使用して、新しい製品ファミリへのアップグレードの状態を取得できます。 このリソースは、Microsoft Azure (MS AZR-0145P) サブスクリプションから Azure プランに顧客をアップグレードするときに適用されます。 要求が成功すると、 [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility)リソースが返されます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証がサポートされます。 パートナーセンター Api でアプリとユーザー認証を使用する場合は、[セキュリティで保護されたアプリモデル](enable-secure-app-model.md)に従います。

- 顧客 ID (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナーセンターの[ダッシュボード](https://partner.microsoft.com/dashboard)で確認できます。 パートナーセンターメニューの [ **CSP** ] を選択し、[ **Customers**] をクリックします。 [Customer] リストから顧客を選択し、[Account] \ (**アカウント**\) を選択します。 お客様のアカウントページで、[**お客様のアカウント情報**] セクションで**Microsoft ID**を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- 製品ファミリ。

- アップグレード要求のアップグレード id。

## <a name="c"></a>C\#

顧客が Azure プランにアップグレードする資格があるかどうかを確認するには、次のようにします。

1. **Product・アップグレード Esrequest**オブジェクトを作成し、製品ファミリとして顧客識別子と "Azure" を指定します。

2. **Iaggregatepartner.customers**コレクションを使用します。

3. **ById**メソッドを呼び出し、**アップグレード id**を渡します。

4. **Checkstatus**メソッドを呼び出し、 **Productupgradesrequest**オブジェクトを渡します。これにより、 **productupgradestatus**オブジェクトが返されます。

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

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法   | 要求 URI |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを使用して、製品のアップグレード状態を取得している顧客を指定します。

| 名前               | Type | 必須 | 説明                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **アップグレード id** | GUID | はい | 値は、GUID 形式のアップグレード識別子です。 この識別子を使用して、追跡するアップグレードを指定できます。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

要求本文には、 [**Productアップグレード**](product-upgrade-resources.md#productupgraderequest)のためのリソースが含まれている必要があります。

### <a name="request-example"></a>要求の例

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

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは本文で[**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility)リソースを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

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
