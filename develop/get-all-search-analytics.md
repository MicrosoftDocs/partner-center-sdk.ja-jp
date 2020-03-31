---
title: すべての検索分析情報を取得する
description: すべての検索分析情報を取得する方法。
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: fc686891cf80e67eab01540a77b3335f23bdc598
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416091"
---
# <a name="get-all-search-analytics-information"></a>すべての検索分析情報を取得する

**適用対象**

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター


顧客向けのすべての検索分析情報を取得する方法。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求の構文**

| メソッド  | 要求 URI |
|---------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1 |

 

**URI パラメーター**


|    パラメーター     |  種類  |                                                                                                                   説明                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      フィルター      | string |                                                                     フィルター条件に一致するデータを返します。 </br> **例:**</br> `.../search?filter=field eq 'value'`                                                                     |
|     groupby      | string |                                         は、用語と日付の両方をサポートしています。 バケット数を制限するショートサーキットロジック。 </br> **例:**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | string | *AggregationLevel*パラメーターには*groupby*が必要です。 *AggregationLevel*パラメーターは、 *groupby*に存在するすべての日付フィールドに適用されます。 </br> **例:**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       [top]        | string |                                                                     ページ数の上限は1万です。 1万未満の値を取得します。  </br> **例:**</br>  `.../search?top=100`                                                                     |
|       skip       | string |                                                                                  スキップする行の数。 </br> **例:**</br> `.../search?top=100&skip=100`                                                                                   |
  
**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

[なし]。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答


成功した場合、応答本文には[検索](partner-center-analytics-resources.md#search_resource)リソースのコレクションが含まれます。

**応答成功およびエラーコード**

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

**応答の例**

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>関連項目
 - [パートナー センターの分析 - リソース](partner-center-analytics-resources.md)
