---
title: 紹介の分析情報をすべて取得する
description: すべての紹介分析情報を取得する方法。
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: b470c59cecf8b214e6d90a244e928e5d15ebd3e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097782"
---
# <a name="get-all-referrals-analytics-information"></a>紹介の分析情報をすべて取得する

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

顧客向けのすべての紹介分析情報を取得する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI |
|---------|-------------|
| **GET** | [* \{ BASEURL \} *](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1 |

### <a name="uri-parameters"></a>URI パラメーター

| パラメーター | Type | 説明 |
|-----------|------|-------------|
| filter | string | フィルター条件に一致するデータを返します。</br> **例:**</br>  `.../referrals?filter=field eq 'value'` |
| groupby | string | は、用語と日付の両方をサポートしています。 バケット数を制限するショートサーキットロジック。</br> **例:**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | string | *AggregationLevel*パラメーターには*groupby*が必要です。 *AggregationLevel*パラメーターは、 *groupby*に存在するすべての日付フィールドに適用されます。</br> **例:**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | string | ページ数の上限は1万です。 1万未満の値を取得します。</br> **例:**</br> `.../referrals?top=100`</br> |
| skip | string | スキップする行の数。</br> **例:**</br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[紹介](partner-center-analytics-resources.md#referrals-resource)リソースのコレクションが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

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

## <a name="see-also"></a>関連項目

- [パートナー センターの分析 - リソース](partner-center-analytics-resources.md)
