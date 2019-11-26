---
title: Azure usage analytics のすべての情報を取得する
description: Azure usage analytics のすべての情報を取得する方法について説明します。
ms.assetid: CDBD04A4-BA34-49B8-9815-7C19253E6C70
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 49df0ac0741ed486ab34015b409eced7fde59afd
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486002"
---
# <a name="get-all-azure-usage-analytics-information"></a>Azure usage analytics のすべての情報を取得する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター


お客様の Azure 使用状況分析に関するすべての情報を取得する方法。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST 要求


**要求の構文**

| メソッド  | 要求 URI |
|---------|-------------|
| **取得** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1 |

 

**URI パラメーター**

<table>
  <thead>
      <th>
        <p>パラメーター</p>
      </th>
      <th>
        <p>種類</p>
      </th>
      <th>
        <p>説明</p>
      </th>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>top</p>
      </td>
      <td>
        <p>string</p>
      </td>
      <td>
        <p>要求で返すデータの行数です。 最大値および指定しない場合の既定値は 10000 です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>skip</p>
      </td>
      <td>
        <p>int</p>
      </td>
      <td>
        <p>クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、<code>top=10000 and skip=0</code> は最初の1万行のデータを取得し、次の1万行のデータを取得 <code>top=10000 and skip=10000</code> ます。</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>filter</p>
      </td>
      <td>
        <p>string</p>
      </td>
      <td>
        <p>要求の <em>filter</em> パラメーターには、応答内の行をフィルター処理する 1 つまたは複数のステートメントが含まれます。 各ステートメントには <strong>eq</strong> 演算子または <strong>ne</strong> 演算子と関連付けられるフィールドと値が含まれ、<strong>and</strong> または <strong>or</strong> を使ってステートメントを組み合わせることができます。 次のフィールドを指定できます。</p>
        <ul>
          <li><em>顧客 Tenantid</em></li>
          <li><em>おける</em></li>
          <li><em>サブスクリプション</em></li>
          <li><em>subscriptionName</em></li>
          <li><em>日付</em></li>
          <li><em>resourceLocation</em></li>
          <li><em>meterCategory</em></li>
          <li><em>meterSubcategory カテゴリ</em></li>
          <li><em>meterUnit</em></li>
          <li><em>reservationOrderId</em></li>
          <li><em>reservationId</em></li>
          <li><em>consumptionMeterId</em></li>
          <li><em>与え</em></li>
        </ul>
        <p><strong>例:</strong></br>
          <code>.../usage/azure?filter=meterCategory eq &#39;Data Management&#39;</code>
        </p>
        <p><strong>例:</strong></br>
          <code>.../usage/azure?filter=meterCategory eq &#39;Data Management&#39; or (usageDate le cast(&#39;2018-01-01&#39;, Edm.DateTimeOffset) and usageDate le cast(&#39;2018-04-01&#39;, Edm.DateTimeOffset))</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>aggregationLevel</p>
      </td>
      <td>
        <p>string</p>
      </td>
      <td>
        <p>集計データを取得する時間範囲を指定します。 次のいずれかの文字列を指定できます。&quot;day&quot;、&quot;week&quot;、または &quot;month&quot;。 指定しない場合、既定値は &quot;day&quot; です。</p>
      <p><em>AggregationLevel</em>パラメーターは、 <em>groupby</em>なしではサポートされていません。 <em>AggregationLevel</em>パラメーターは、 <em>groupby</em>に存在するすべての日付フィールドに適用されます。</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>orderby</p>
      </td>
      <td>
        <p>string</p>
      </td>
      <td>
        <p>各インストールの結果データ値の順序を指定するステートメントです。 構文は、<em>フィールド</em>パラメーターには、次のいずれかの文字列を <code>...&orderby=field [order],field [order],...</code> ます。</p>
        <ul>
          <li>&quot;の顧客 Tenantid&quot;</li>
          <li>&quot;様&quot;</li>
          <li>subscriptionId&quot; の &quot;</li>
          <li>&quot;subscriptionName&quot;</li>
          <li>&quot;の&quot; 日付</li>
          <li>&quot;resourceLocation&quot;</li>
          <li>&quot;meterCategory&quot;</li>
          <li>&quot;meterSubcategory カテゴリ&quot;</li>
          <li>&quot;meterUnit&quot;</li>
          <li>&quot;reservationOrderId&quot;</li>
          <li>&quot;reservationId&quot;</li>
          <li>&quot;consumptionMeterId&quot;</li>
          <li>&quot;serviceType&quot;</li>
        </ul>
        <p><em>Order</em>パラメーターは省略可能であり、&quot;asc&quot; または &quot;desc&quot; を使用して、各フィールドの昇順または降順を指定できます。 既定値は &quot;asc&quot; です。</p>
        <p><strong>例:</strong><br/> 
          <code>...&orderby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>groupby</p>
      </td>
      <td>
        <p>string</p>
      </td>
      <td>
        <p>指定したフィールドのみにデータ集計を適用するステートメントです。 次のフィールドを指定できます。</p>
        <ul>
          <li><em>顧客 Tenantid</em></li>
          <li><em>おける</em></li>
          <li><em>サブスクリプション</em></li>
          <li><em>subscriptionName</em></li>
          <li><em>日付</em></li>
          <li><em>resourceLocation</em></li>
          <li><em>meterCategory</em></li>
          <li><em>meterSubcategory カテゴリ</em></li>
          <li><em>meterUnit</em></li>
          <li><em>reservationOrderId</em></li>
          <li><em>reservationId</em></li>
          <li><em>consumptionMeterId</em></li>
          <li><em>与え</em></li>
        </ul>
        <p>返されるデータ行には、 <em>groupby</em>パラメーターで指定されたフィールドと<em>数量</em>が含まれます。</p>
        <p><em>groupby</em> パラメーターは、<em>aggregationLevel</em> パラメーターと同時に使用できます。</p>
        <p><strong>例:</strong></br>
          <code>...&groupby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>


**要求ヘッダー**

- 詳細については、「[ヘッダー](headers.md) 」を参照してください。

**要求本文**

なし。

**要求の例**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答


成功した場合、応答本文には[Azure の使用](partner-center-analytics-resources.md#azure_usage)リソースのコレクションが含まれます。

**応答成功およびエラーコード**

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

**応答の例**

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20  
}
```


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>関連項目
  - [パートナーセンター分析-リソース](partner-center-analytics-resources.md)

