---
title: パートナーライセンスの使用状況情報の取得
description: パートナーライセンスの使用状況情報を収集して、すべての顧客を含める方法。
ms.assetid: 87BCC8FC-5C29-4245-8607-BB62ABC03EDE
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: dfecb0dc90253f2d13f645ab89fe98eeec3c2164
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488502"
---
# <a name="get-partner-licenses-usage-information"></a>パートナーライセンスの使用状況情報の取得

**適用対象**

- パートナー センター

パートナーライセンスの使用状況情報を収集して、すべての顧客を含める方法。

> [!NOTE]
> このシナリオは、[ライセンスの取得の使用状況に関する情報](get-licenses-usage-information.md)に置き換えられます。


## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報を使用した認証がサポートされます。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


ライセンスの展開の集計データを取得するには、まず、 [**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.analytics)プロパティからパートナーレベルの分析コレクション操作へのインターフェイスを取得します。 次に、[[**ライセンス**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses)] プロパティから、パートナーレベルのライセンス分析コレクションへのインターフェイスを取得します。 最後に、 [**usage. get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get)メソッドを呼び出して、ライセンスの使用状況に関する集計データを取得します。 メソッドが成功した場合は、 [**PartnerLicensesUsageInsights**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights)オブジェクトのコレクションが取得されます。

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesUsageAnalytics = partnerOperations.Analytics.Licenses.Usage.Get();
```

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求の構文**

| メソッド  | 要求 URI                                                                      |
|---------|----------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1 |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答

成功した場合、応答本文には、使用されたライセンスに関する情報を提供する[PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights)リソースのコレクションが含まれます。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
HTTP/1.1 200 OK
Content-Length: 1156
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CV: wk0/vjugzEe0Z9cv.0
MS-ServerId: 101112012
Date: Wed, 15 Mar 2017 01:18:26 GMT

{
    "totalCount": 5,
    "items": [{
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Microsoft Dynamics CRM",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```