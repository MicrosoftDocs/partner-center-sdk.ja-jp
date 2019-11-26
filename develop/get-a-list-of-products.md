---
title: Get a list of products (by country)
description: You can use the Product resource to get a collection of products by customer country.
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 4f3f00db59fa06769a581fca6ea028bc94f61883
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487322"
---
# <a name="get-a-list-of-products-by-country"></a>Get a list of products (by country)

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

You can use the following methods to get a collection of products available in a particular country.

## <a name="prerequisites"></a>前提条件

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A country.

## <a name="c"></a>C\#

To get a list of products:

1. Use your **IAggregatePartner.Products** collection to select the country by using the **ByCountry()** method.
2. Select the catalog view using the **ByTargetView()** method.
3. (Optional) Select the reservation scope using the **ByReservationScope()** method.
3. (Optional) Select the target segment using the **ByTargetSegment()** method.
4. Call the **Get()** or **GetAsync()** method to return the collection.

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

### <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

To get a list of products:

1. Use your **IAggregatePartner.getProducts** function to select the country by using the **byCountry()** function.
2. Select the catalog view using the **byTargetView()** function.
3. (Optional) Select the target segment using the **byTargetSegment()** function.
4. Call the **get()** function to return the collection.

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

### <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

To get a list of products:

1. Execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command.
2. Select the catalog by specifying the **Catalog** parameter.
3. (Optional) Select the target segment by specifying the **Segment** parameter.

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest"></a>REST

### <a name="rest-request"></a>Rest request

#### <a name="request-syntax"></a>要求の構文

| メソッド  | 要求 URI                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1 |

##### <a name="uri-parameters"></a>URI パラメーター

Use the following path and query parameters to get a list of products.

| 名前                   | タスクバーの検索ボックスに     | 必須かどうか | 説明                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| country                | string   | [はい]      | The country/region ID.                                                  |
| targetView             | string   | [はい]      | Identifies the target view of the catalog. The supported values are: <ul><li>**Azure**, which includes all Azure items</li><li>**AzureReservations**, which includes all Azure reservation items</li><li>**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</li><li>**AzureReservationsSQL**, which includes all SQL reservation items</li><li>**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</li><li>**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</li><li>**OnlineServices**, which includes all online service items (including commercial marketplace products)</li><li>**Software**, which includes all software items</li><li>**SoftwareSUSELinux**, which includes all software SUSE Linux items</li><li>**SoftwarePerpetual**, which includes all perpetual software items</li><li>**SoftwareSubscriptions**, which includes all software subscription items</li></ul> |
| targetSegment          | string   | 必須ではない       | Identifies the target segment. The view for different target audiences. The supported values are: <ul><li>**commercial**</li><li>**education**</li><li>**government**</li><li>**nonprofit**</li></ul> |
| reservationScope | string   | 必須ではない | When querying for a list of products for Azure Reservations, specify `reservationScope=AzurePlan` to get a list of products that are applicable to Azure plans. Exclude this parameter to get a list of products for Azure reservations, which are applicable to Microsoft Azure (**MS-AZR-0145P**) subscriptions.  |

#### <a name="request-headers"></a>要求ヘッダー

For more information, see [Headers](headers.md).

#### <a name="request-body"></a>要求本文

なし。

#### <a name="request-examples"></a>要求の例

##### <a name="products-by-country"></a>Products by country

Follow this example to get a list of products by country for Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

##### <a name="azure-vm-reservations-azure-plan"></a>Azure VM reservations (Azure plan)

Follow this example to get a list of products by country for Azure VM reservations that are applicable to Azure plans.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

##### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Azure VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions

Follow this example to get a list of products by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

### <a name="rest-response"></a>REST response

If successful, the response body contains a collection of [**Product**](product-resources.md#product) resources.

#### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

This method returns the following error codes:

| HTTP 状態コード     | エラー コード   | 説明                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Access to the requested targetSegment is not allowed.                                                     |
| 403                  | 400036       | Access to the requested targetView is not allowed.                                                        |

#### <a name="response-example"></a>応答の例

```http
{
    "totalCount": 19,
    "items": [
        {
            "id": "DZH318Z0BQ3Q",
            "title": "Virtual Machines DSv2 Series",
            "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
            "productType": {
                "id": "Azure",
                "displayName": "Azure",
                "subType": {
                "id": "VirtualMachines",
                "displayName": "VirtualMachines"
                }
            },
            "isMicrosoftProduct": true,
            "publisherName": "Microsoft",
            "links": {
                "skus": {
                    "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
