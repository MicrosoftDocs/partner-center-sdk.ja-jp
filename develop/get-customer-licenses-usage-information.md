---
title: カスタマーライセンスの使用状況情報を取得する
description: 特定の顧客のライセンス使用状況の洞察を取得する方法。
ms.assetid: 02B98495-9FE7-4A9F-B1DD-B14563D0FF29
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 6b8230ae3ab8927e1c599318e60a55ca866d1a9f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486352"
---
# <a name="get-customer-licenses-usage-information"></a>カスタマーライセンスの使用状況情報を取得する


**適用対象**

- パートナー センター

特定の顧客に対してライセンスを取得する方法について説明します。

> [!NOTE]
> このシナリオは、[ライセンスの取得の使用状況に関する情報](get-licenses-usage-information.md)に置き換えられます。


## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件

「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報を使用した認証がサポートされます。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


指定された顧客のデプロイに関する集計データを取得するには、まず顧客 ID を指定して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出し、顧客を識別します。 次に、 [**analytics**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics)プロパティから顧客レベルの分析コレクション操作へのインターフェイスを取得します。 次に、[[**ライセンス**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses)] プロパティから顧客レベルのライセンス分析コレクションへのインターフェイスを取得します。 最後に、 [**usage. get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get)メソッドを呼び出して、ライセンスの使用状況に関する集計データを取得します。 メソッドが成功した場合は、 [**CustomerLicensesUsageInsights**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights)オブジェクトのコレクションが取得されます。

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Usage.Get();
```

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求の構文**

| メソッド  | 要求 URI                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/usage HTTP/1.1 |

 

**URI パラメーター**

顧客を識別するには、次のパスパラメーターを使用します。

| 名前        | 種類 | 必須 | 説明                                                |
|-------------|------|----------|------------------------------------------------------------|
| 顧客 id | guid | 〇      | 顧客を識別する GUID 形式の顧客 id。 |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f657d2a8-9ed6-41b4-abfc-3cf4abebd62f
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答


成功した場合、応答本文には、ライセンスの使用状況に関する情報を提供する[CustomerLicensesUsageInsights](analytics-resources.md#customerlicensesusageinsights)リソースのコレクションが含まれます。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 1726
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: f657d2a8-9ed6-41b4-abfc-3cf4abebd62f
MS-CV: 0mufM0K1kEOoR7oI.0
MS-ServerId: 030020525
Date: Wed, 15 Mar 2017 01:19:58 GMT

{
    "totalCount": 5,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesActive": 0,
            "licensesQualified": 5,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesActive": 0,
            "licensesQualified": 2,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 




