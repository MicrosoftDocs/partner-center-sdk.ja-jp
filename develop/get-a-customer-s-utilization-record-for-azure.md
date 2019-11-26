---
title: Get a customer's utilization records for Azure
description: You can use the Azure utilization API to get the utilization records of a customer's Azure subscription for a specified time period.
ms.assetid: 0270DBEA-AAA3-46FB-B5F0-D72B9BAC3112
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 825b5ea8c65d5ae52979ca5b412f36dfdff8ab59
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489592"
---
# <a name="get-a-customers-utilization-records-for-azure"></a>Get a customer's utilization records for Azure

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

You can get the utilization records of a customer's Azure subscription for a specified time period using the Azure utilization API.

## <a name="prerequisites"></a>前提条件

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone app and App+User credentials.
- A customer identifier.
- A subscription identifier.

This API returns daily and hourly unrated consumption for an arbitrary time span. However, *this API is not supported for Azure plans*. If you have an Azure plan, see the articles [Get invoice unbilled consumption line items](get-invoice-unbilled-consumption-lineitems.md) and [Get invoice billed consumption line items](get-invoice-billed-consumption-lineitems.md) instead. These articles describe how to get rated consumption at daily level per meter per resource. This is equivalent to the daily grain data provided by the Azure utilization API. You will need to use the invoice identifier to retrieve billed usage data. Or, you can use current and previous periods to get unbilled usage estimates. *Hourly grain data and arbitrary date range filters aren't currently supported for Azure plan subscription resources*.

## <a name="azure-utilization-api"></a>Azure Utilization API

This Azure utilization API provides access to utilization records for a time period that represents when the utilization was reported in the billing system. It provides access to the same utilization data that is used to create and calculate the reconciliation file. However, it does not have knowledge of billing system reconciliation file logic. You should not expect reconciliation file summary results to match the result retrieved from this API exactly for the same time period.

For example, the billing system takes the same utilization data and applies lateness rules to determine what is accounted for in a reconciliation file. When a billing period closes, all usage until the end of the day that the billing period ends is included in the reconciliation file. Any late usage within the billing period that is reported within 24 hours after the billing period ends is accounted for in the next reconciliation file. For the lateness rules of how the partner is billed, see [Get consumption data for an Azure subscription](https://docs.microsoft.com/previous-versions/azure/reference/mt219001(v=azure.100)).

This REST API is paged. If the response payload is larger than a single page, you must follow the next link to get the next page of utilization records.

## <a name="c"></a>C\#

To obtain the Azure Utilization Records:

1. Get the customer ID and subscription ID. 
2. Call the [**IAzureUtilizationCollection.Query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) method to return a [**ResourceCollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) that contains the utilization records. 
3. Obtain an Azure utilization record enumerator to traverse the utilization pages. You must do this because the resource collection is paged.

- **Sample**: [Console test app](console-test-app.md)
- **Project**: Partner Center SDK Samples
- **Class**: GetAzureSubscriptionUtilization.cs

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier. You then call the **IAzureUtilizationCollection.query** function to return a **ResourceCollection** that contains the utilization records. Because the resource collection is paged, you must then obtain an Azure utilization record enumerator to traverse the utilization pages.

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

To obtain the Azure Utilization Records, you first need a customer identifier and a subscription identifier. You then call the [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md). This command will return all records available for the specified period of time.

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest"></a>REST

### <a name="rest-request"></a>REST request

#### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI |
|------- | ----------- |
| **GET** | *{baseURL}* /v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start\_time={start-time}&end\_time={end-time}&granularity={granularity}&show\_details={True} |

##### <a name="uri-parameters"></a>URI パラメーター

Use the following path and query parameters to get the utilization records.

| 名前 | タスクバーの検索ボックスに | 必須かどうか | 説明 |
| ---- | ---- | -------- | ----------- |
| customer-tenant-id | string | [はい] | A GUID-formatted string that identifies the customer. |
| subscription-id | string | [はい] | A GUID-formatted string that identifies the subscription. |
| start_time | string in UTC date-time offset format | [はい] | The start of the time range that represents when the utilization was reported in the billing system. |
| end_time | string in UTC date-time offset format | [はい] | The end of the time range that represents when the utilization was reported in the billing system. |
| granularity | string | 必須ではない | Defines the granularity of usage aggregations. Available options are: `daily` (default) and `hourly`.
| show_details | boolean | 必須ではない | Specifies whether to get the instance-level usage details. 既定値は `true` です。 |
| size | number | 必須ではない | Specifies the number of aggregations returned by a single API call. The default is 1000. The max is 1000. |

#### <a name="request-headers"></a>要求ヘッダー

See [Partner Center REST headers](headers.md) for more information.

#### <a name="request-body"></a>要求本文

なし

#### <a name="request-example"></a>要求の例

The following example request produces results similar to what the reconciliation file will show for the period 7/2 - 8/1. These results may not match exactly (see the section [Azure utilization API](#azure-utilization-api) for details).

This example request returns utilization data reported in the billing system between 7/2 at 12 AM (UTC) and 8/2 at 12 AM (UTC).

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="rest-response"></a>REST response

If successful, this method returns a collection of [Azure Utilization Record](azure-utilization-record-resources.md) resources in the response body. If the Azure utilization data is not yet ready in a dependent system, this method returns an HTTP Status Code 204 with a Retry-After header.

#### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read the HTTP status code, [error code type](error-codes.md), and additional parameters.

#### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
