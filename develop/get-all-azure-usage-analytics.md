---
title: Azure の使用量分析情報をすべて取得する
description: Azure usage analytics のすべての情報を取得する方法について説明します。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c6302a2223bbb9c56943b04175a9cba44db1d1d2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095237"
---
# <a name="get-all-azure-usage-analytics-information"></a>Azure の使用量分析情報をすべて取得する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

お客様の Azure 使用状況分析に関するすべての情報を取得する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI |
|---------|-------------|
| **GET** | [* \{ BASEURL \} *](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1 |

### <a name="uri-parameters"></a>URI パラメーター

<table>
  <thead>
      <th>
        <p>パラメーター</p>
      </th>
      <th>
        <p>Type</p>
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
        <p>クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、は、 <code>top=10000 and skip=0</code> 最初の1万行のデータを取得し、 <code>top=10000 and skip=10000</code> 次の1万行のデータを取得します。</p>
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
        <p>要求の <em>filter</em> パラメーターには、応答内の行をフィルター処理する 1 つまたは複数のステートメントが含まれます。 各ステートメントには、または演算子に関連付けられたフィールドと値が含まれて <strong> <code>eq</code> </strong> <strong> <code>ne</code> </strong> おり、ステートメント <strong> <code>and</code> </strong> はまたはを使用して組み合わせることができ <strong> <code>or</code> </strong> ます。 次のものを指定できます。</p>
        <ul>
          <li><code>customerTenantId</code></li>
          <li><code>customerName</code></li>
          <li><code>subscriptionId</code></li>
          <li><code>subscriptionName</code></li>
          <li><code>usageDate</code></li>
          <li><code>resourceLocation</code></li>
          <li><code>meterCategory</code></li>
          <li><code>meterSubcategory</code></li>
          <li><code>meterUnit</code></li>
          <li><code>reservationOrderId</code></li>
          <li><code>reservationId</code></li>
          <li><code>consumptionMeterId</code></li>
          <li><code>serviceType</code></li>
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
        <p>集計データを取得する時間範囲を指定します。 <code>day</code>には、、 <code>week</code> 、またはのいずれかの文字列を指定できます <code>month</code> 。 指定されていない場合、既定値は <code>day</code> です。</p>
      <p><code>aggregationLevel</code>パラメーターは、なしではサポートされません <code>groupby</code> 。 <code>aggregationLevel</code>パラメーターは、に存在するすべての日付フィールドに適用され <code>groupby</code> ます。</p>
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
        <p>各インストールの結果データ値の順序を指定するステートメントです。 構文は <code>...&orderby=field [order],field [order],...</code>です。 パラメーターには <code>field</code> 、次のいずれかの文字列を指定できます。</p>
        <ul>
          <li><code>customerTenantId</code></li>
          <li><code>customerName</code></li>
          <li><code>subscriptionId</code></li>
          <li><code>subscriptionName</code></li>
          <li><code>usageDate</code></li>
          <li><code>resourceLocation</code></li>
          <li><code>meterCategory</code></li>
          <li><code>meterSubcategory</code></li>
          <li><code>meterUnit</code></li>
          <li><code>reservationOrderId</code></li>
          <li><code>reservationId</code></li>
          <li><code>consumptionMeterId</code></li>
          <li><code>serviceType</code></li>
        </ul>
        <p><em>Order</em>パラメーターは省略可能であり、 <code>asc</code> またはにすることができます。 <code>desc</code> 各フィールドの昇順または降順を指定します。 既定値は、<code>asc</code> です。</p>
        <p><strong>例:</strong><br/>
          <code>...&orderby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>groupby</code></p>
      </td>
      <td>
        <p>string</p>
      </td>
      <td>
        <p>指定したフィールドのみにデータ集計を適用するステートメントです。 次のフィールドを指定できます。</p>
        <ul>
          <li><code>customerTenantId</code></li>
          <li><code>customerName</code></li>
          <li><code>subscriptionId</code></li>
          <li><code>subscriptionName</code></li>
          <li><code>usageDate</code></li>
          <li><code>resourceLocation</code></li>
          <li><code>meterCategory</code></li>
          <li><code>meterSubcategory</code></li>
          <li><code>meterUnit</code></li>
          <li><code>reservationOrderId</code></li>
          <li><code>reservationId</code></li>
          <li><code>consumptionMeterId</code></li>
          <li><code>serviceType</code></li>
        </ul>
        <p>返されるデータ行には、パラメーターに指定されたフィールドと数量が含まれ <code>groupby</code> ます。 <em>Quantity</em></p>
        <p>パラメーターは、 <code>groupby</code> パラメーターと共に使用でき <code>aggregationLevel</code> ます。</p>
        <p><strong>例:</strong></br>
          <code>...&groupby=meterCategory,meterUnit</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[Azure の使用](partner-center-analytics-resources.md#csp-program-azure-usage-analytics)リソースのコレクションが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

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

## <a name="see-also"></a>関連項目

- [パートナー センターの分析 - リソース](partner-center-analytics-resources.md)
