---
title: 顧客のサービスコストの明細項目を取得する
description: 指定された請求期間の顧客のサービスコスト明細項目を取得します。
ms.assetid: 1D6364A2-51FE-44E4-96A0-444EDB3BB56A
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7393c3f4c200fa6f156b9a5fbc730b5bcb390dc7
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74490152"
---
# <a name="get-a-customers-service-costs-line-items"></a>顧客のサービスコストの明細項目を取得する

適用対象:

- パートナー センター

指定された請求期間の顧客のサービスコスト明細項目を取得します。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報を使用した認証がサポートされます。
- 顧客識別子。
- 請求期間インジケーター (**最新**)。

## <a name="c"></a>C\#

指定された顧客のサービスコストの概要を取得するには:

1. 顧客 ID を指定して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出し、顧客を識別します。
2. [**ServiceCosts**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts)プロパティを使用して、顧客サービスコストの収集操作へのインターフェイスを取得します。
3. [**ServiceCostsBillingPeriod**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod)列挙体のメンバーを使用して[**By の期間**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod)メソッドを呼び出し、 [**IServiceCostsCollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection)を返します。
4. 顧客のサービスコストの明細項目を取得するには、 [**IServiceCostsCollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get)または[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync)メソッドを使用します。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).LineItems.Get();
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド  | 要求 URI                                                                                                             |
|---------|-------------------------------------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period}/lineitems HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

次のパスパラメーターを使用して、顧客と請求期間を識別します。

| 名前           | 種類   | 必須 | 説明                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| 顧客 id    | guid   | 〇      | 顧客を識別する GUID 形式の顧客 ID。                                                                       |
| 請求-期間 | string | 〇      | 請求期間を表すインジケーター。 唯一サポートされている値は、最新です。 文字列の大文字と小文字の区別は関係ありません。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent/lineitems HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には、サービスのコストに関する情報を提供する[ServiceCostLineItem](service-costs-resources.md)リソースが含まれます。

> [!IMPORTANT]
> 次のプロパティは、製品が1回だけ*購入*されるサービスコスト明細項目 ( **productId**、 **productName**、 **skuId**、 **skuname**、 **availabilityId**、 **publisherId**、 **publishername**、 **termandbil**、 **discountdetails**)*にのみ適用*されます。 これらのプロパティは、製品が*定期的に購入*されるサービスライン項目には適用され*ません*。 たとえば、これらのプロパティは、サブスクリプションベースの Office 365 および Azure には適用され*ません*。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 2148
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "attributes": {
        "objectType": "Collection"
    },
    "items":
    [{
            "afterTaxTotal": 0.0,
            "chargeType": "PURCHASE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-01-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 0.0,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2015-12-15T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 0.0,
            "invoiceNumber": "T000003163",
            "invoiceType": "OneTime",
            "productId": "DZH318Z0BJR6",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BMFK",
            "productName": "Azure Managed Experience",
            "skuName": "Azure Managed Experience - Optimize",
            "publisherName": "Microsoft",
            "publisherId": "01323244",
            "termAndBillingCycle": "",
            "discountDetails": "N/A"
        }, {
            "afterTaxTotal": 17.219999999999999,
            "chargeType": "CYCLE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-02-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 17.219999999999999,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2016-01-12T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 17.219999999999999,
            "invoiceNumber": "D000003163",
            "invoiceType": "Recurring",
            "productId": "DZH318Z0BJR7",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BTTTT",
            "productName": "NGINX Plus",
            "skuName": "NGINX Plus (Ubuntu 14.04)",
            "publisherName": ""Nginx, Inc.",
            "publisherId": "212336222",
            "termAndBillingCycle": "30 Days Trial",
            "discountDetails": "20%"
        }
    ],
    "links": {
        "self": {
            "headers": [],
            "method": "GET",
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems"
        }
    },
    "totalCount": 2
}
```
