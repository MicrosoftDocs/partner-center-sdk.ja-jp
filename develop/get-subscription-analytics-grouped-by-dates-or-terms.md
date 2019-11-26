---
title: Get subscription analytics grouped by dates or terms
description: How to get subscription analytics information grouped by dates or terms.
ms.assetid: 5D0C0649-F64D-40A9-ACCC-2077E2D2BA4E
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 15387d0cbf00917628a4f401094c23458e59064c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487162"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>Get subscription analytics grouped by dates or terms

**Applies To**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター


How to get subscription analytics information for your customers grouped by dates or terms.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only.


## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request


**Request syntax**

| メソッド | 要求 URI |
|--------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries} |

 
**URI parameters**

Use the following required path parameters to identify your organization and to group the results.

| 名前 | タスクバーの検索ボックスに | 必須かどうか | 説明 |
|------|------|----------|-------------|
| groupby_queries | pairs of strings and dateTime | [はい] | The terms and dates to filter the result. |

 

**GroupBy syntax**

The group by parameter must be composed as a series of comma separated, field values.

An unencoded example looks like this:  

```http
?groupby=termField1,dateField1,termField2
```

The following table shows a list of the supported fields for group by.

| フィールド | タスクバーの検索ボックスに | 説明 |
|-------|------|-------------|
| customerTenantId | string | A GUID-formatted string that identifies the customer tenant. |  
| customerName | string | The name of the customer. |  
| customerMarket | string | The country/region that the customer does business in. |  
| id | string | A GUID-formatted string that identifies the subscription. |  
| status | string | The subscription status. Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED". |  
| productName | string | 製品の名前。 |  
| subscriptionType | string | The subscription type. Note: This field is case sensitive. Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |  
| autoRenewEnabled | Boolean | A value indicating whether the subscription is renewed automatically. |  
| partnerId  | string | The MPN ID. For a direct reseller, this will be the MPN ID of the partner. For an indirect reseller, this will be the MPN ID of the indirect reseller. |  
| friendlyName | string | The name of the subscription. |  
| partnerName | string | Name of the partner for whom the subscription was purchased |  
| providerName | string | When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.
| creationDate | string in UTC date time format | The date the subscription was created. |  
| effectiveStartDate | string in UTC date time format | The date the subscription starts. |  
| commitmentEndDate | string in UTC date time format | The date the subscription ends. |  
| currentStateEndDate | string in UTC date time format | The date that the current status of the subscription will change. |  
| trialToPaidConversionDate | string in UTC date time format | The date that the subscription converts from trial to paid. 既定値は null です。 |  
| trialStartDate | string in UTC date time format | The date that the trial period for the subscription started. 既定値は null です。 |  
| lastUsageDate | string in UTC date time format | The date that the subscription was last used. 既定値は null です。 |  
| deprovisionedDate | string in UTC date time format | The date that the subscription was deprovisioned. 既定値は null です。 |  
| lastRenewalDate | string in UTC date time format | The date that the subscription was last renewed. 既定値は null です。 |  

**Filter fields**

The following table lists optional filter fields and their descriptions:

| フィールド | タスクバーの検索ボックスに |  説明 |
|-------|------|--------------|
| top | 整数 | 要求で返すデータの行数です。 If the value is not specified, the maximum value and the default value are 10000. クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。 |
| skip | 整数 | クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data. |
| filter | string | 応答内の行をフィルター処理する 1 つまたは複数のステートメントです。 Each filter statement contains a field name from the response body and a value that are associated with the **eq**, **ne**, or for certain fields, the **contains** operator. **and** または **or** を使ってステートメントを組み合わせることができます。 String values must be surrounded by single quotes in the filter parameter. See the following section for a list of fields that can be filtered and the operators that are supported with those fields. |
| aggregationLevel | string | 集計データを取得する時間範囲を指定します。 次のいずれかの文字列を指定できます。**day**、**week**、または **month**。 If the value is not specified, the default is **dateRange**. **Note**: This parameter applies only when a date field is passed as part of the groupBy parameter. |
| groupBy | string | 指定したフィールドのみにデータ集計を適用するステートメントです。 |


**Request headers**

- See [Headers](headers.md) for more information.

**Request body**

なし。

**Request example**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType  
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>REST Response

If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription) resources grouped by the specified terms and dates.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>See also

 - [Partner Center Analytics - Resources](partner-center-analytics-resources.md)