---
title: 検索の分析情報をすべて取得する
description: すべての検索分析情報を取得する方法。
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 10e607a0fd2c973909c4b8aa57d6c7074eab9503
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156564"
---
# <a name="get-all-search-analytics-information"></a>検索の分析情報をすべて取得する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

顧客向けのすべての検索分析情報を取得する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI |
|---------|-------------|
| **GET** | baseURL/partner/v1/analytics/search HTTP/1.1 [* \{\}*](partner-center-rest-urls.md) |

### <a name="uri-parameters"></a>URI パラメーター

|    パラメーター     |  Type  |                                                                                                                   説明                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      filter      | string |                                                                     フィルター条件に一致するデータを返します。 </br> **例:**</br> `.../search?filter=field eq 'value'`                                                                     |
|     groupby      | string |                                         は、用語と日付の両方をサポートしています。 バケット数を制限するショートサーキットロジック。 </br> **例:**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | string | *AggregationLevel*パラメーターには*groupby*が必要です。 *AggregationLevel*パラメーターは、 *groupby*に存在するすべての日付フィールドに適用されます。 </br> **例:**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       top        | string |                                                                     ページ数の上限は1万です。 1万未満の値を取得します。  </br> **例:**</br>  `.../search?top=100`                                                                     |
|       skip       | string |                                                                                  スキップする行の数。 </br> **例:**</br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[検索](partner-center-analytics-resources.md#search-resource)リソースのコレクションが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

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

## <a name="see-also"></a>関連項目

- [パートナー センターの分析 - リソース](partner-center-analytics-resources.md)
