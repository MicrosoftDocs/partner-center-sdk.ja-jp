---
title: すべての紹介分析情報を取得する
description: すべての紹介分析情報を取得する方法。
ms.assetid: C6051714-1D8A-4448-9705-12AEC9A6420E
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: d5ad0ad0eedcce633940daa6356e2a2e1e9220c5
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485952"
---
# <a name="get-all-referrals-analytics-information"></a>すべての紹介分析情報を取得する

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター


顧客向けのすべての紹介分析情報を取得する方法。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求の構文**

| メソッド  | 要求 URI |
|---------|-------------|
| **取得** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1 |
 

**URI パラメーター**

| パラメーター | 種類 | 説明 |
|-----------|------|-------------|
| filter | string | フィルター条件に一致するデータを返します。</br> **例:**</br>  `.../referrals?filter=field eq 'value'` |
| groupby | string |    は、用語と日付の両方をサポートしています。 バケット数を制限するショートサーキットロジック。</br> **例:**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | string |   *AggregationLevel*パラメーターには*groupby*が必要です。 *AggregationLevel*パラメーターは、 *groupby*に存在するすべての日付フィールドに適用されます。</br> **例:**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | string | ページ数の上限は1万です。 1万未満の値を取得します。</br> **例:**</br> `.../referrals?top=100`</br> |
| skip | string |   スキップする行の数。</br> **例:**</br>  `.../referrals?top=100&skip=100` |

  
**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答


成功した場合、応答本文には[紹介](partner-center-analytics-resources.md#referrals)リソースのコレクションが含まれます。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>関連項目
 - [パートナーセンター分析-リソース](partner-center-analytics-resources.md)
