---
title: 間接顧客の分析情報をすべて取得する
description: すべての間接リセラーの分析情報を取得する方法。
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 4a8bf1a958b28b5ea8c471a3bbee9009243f7455
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157774"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>間接顧客の分析情報をすべて取得する

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

顧客向けの間接リセラー分析に関するすべての情報を取得する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI |
|---------|-------------|
| **GET** | baseURL/partner/v1/analytics/indirectresellers HTTP/1.1 [* \{\}*](partner-center-rest-urls.md) |

### <a name="uri-parameters"></a>URI パラメーター

<table>
<thead>
    <th>パラメーター</th>
    <th>Type</th>
    <th>説明</th>
</thead>
<tbody>
    <tr>
        <td>partnerTenantId</td>
        <td>string</td>
        <td>間接リセラーデータを取得するパートナーのテナント ID。 </td>
    </tr>
    <tr>
        <td>id</td>
        <td>string</td>
        <td>間接リセラー ID</td>
    </tr>
    <tr>
        <td>name</td>
        <td>string</td>
        <td>間接リセラーデータを取得するパートナーの名前。</td>
    </tr>
    <tr>
        <td>market</td>
        <td>string</td>
        <td>間接リセラーデータを取得するパートナーの市場。</td>
    </tr>
    <tr>
        <td>firstSubscriptionCreationDate</td>
        <td>UTC 日時形式の文字列</td>
        <td>間接リセラーデータを取得する最初のサブスクリプションの作成日。</td>
    </tr>
    <tr>
        <td>latestSubscriptionCreationDate</td>
        <td>UTC 日時形式の文字列</td>
        <td>最新のサブスクリプションの作成日。</td>
    </tr>
    <tr>
        <td>firstSubscriptionEndDate</td>
        <td>UTC 日時形式の文字列</td>
        <td>サブスクリプションが初めて終了したとき。</td>
    </tr>
    <tr>
        <td>latestSubscriptionEndDate</td>
        <td>UTC 日時形式の文字列</td>
        <td>任意のサブスクリプションが終了した最後の日付。 </td>
    </tr>
    <tr>
        <td>firstSubscriptionSuspendedDate</td>
        <td>UTC 日時形式の文字列</td>
        <td>サブスクリプションが初めて中断されたとき。</td>
    </tr>
    <tr>
        <td>latestSubscriptionSuspendedDate</td>
        <td>UTC 日時形式の文字列</td>
        <td>サブスクリプションが中断された最後の日付。</td>
    </tr>
    <tr>
        <td>firstSubscriptionDeprovisionedDate</td>
        <td>UTC 日時形式の文字列</td>
        <td>サブスクリプションが初めてプロビジョニング解除されたとき。</td>
    </tr>
    <tr>
        <td>latestSubscriptionDeprovisionedDate</td>
        <td>UTC 日時形式の文字列</td>
        <td>サブスクリプションがプロビジョニング解除された最後の日付。</td>
    </tr>
    <tr>
        <td>subscriptionCount</td>
        <td>double</td>
        <td>すべての付加価値再販業者のサブスクリプション数</td>
    </tr>
    <tr>
        <td>licenseCount</td>
        <td>double</td>
        <td>すべての付加価値再販業者のライセンス数</td>
    </tr>
    <tr>
        <td>indirectResellerCount</td>
        <td>double</td>
        <td>間接リセラー数</td>
    </tr>
    <tr>
        <td>top</td>
        <td>string</td>
        <td>要求で返すデータの行数です。 最大値および指定しない場合の既定値は 10000 です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。</td>
    </tr>
    <tr>
        <td>skip</td>
        <td>int</td>
        <td>
          <p>クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、は<code>top=10000 and skip=0</code> 、最初の1万行のデータを<code>top=10000 and skip=10000</code>取得し、次の1万行のデータを取得します。</p>
        </td>
    </tr>
    <tr>
        <td>filter</td>
        <td>string</td>
        <td>
            <p>要求の <em>filter</em> パラメーターには、応答内の行をフィルター処理する 1 つまたは複数のステートメントが含まれます。 各ステートメントには <strong>eq</strong> 演算子または <strong>ne</strong> 演算子と関連付けられるフィールドと値が含まれ、<strong>and</strong> または <strong>or</strong> を使ってステートメントを組み合わせることができます。 次のフィールドを指定できます。</p>
            <ul>
                <li><em>partnerTenantId</em></li>
                <li><em>id</em></li>
                <li><em>名前</em></li>
                <li><em>マーケティング</em></li>
                <li><em>firstSubscriptionCreationDate</em></li>
                <li><em>latestSubscriptionCreationDate</em></li>
                <li><em>firstSubscriptionEndDate</em></li>
                <li><em>latestSubscriptionEndDate</em></li>
                <li><em>firstSubscriptionSuspendedDate</em></li>
                <li><em>latestSubscriptionSuspendedDate</em></li>
                <li><em>firstSubscriptionDeprovisionedDate</em></li>
                <li><em>latestSubscriptionDeprovisionedDate</em></li>
            </ul>
            <p><strong>例:</strong></br>
              <code>.../indirectresellers?filter=market eq &#39;US&#39;</code></p>
            <p><strong>例:</strong></br>
                <code>.../indirectresellers?filter=market eq &#39;US&#39; or (firstSubscriptionCreationDate le cast(&#39;2018-01-01&#39;,Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast(&#39;2018-04-01&#39;,Edm.DateTimeOffset))</code>
            </p>
        </td>
    </tr>
    <tr>
        <td>aggregationLevel</td>
        <td>string</td>
        <td><p>集計データを取得する時間範囲を指定します。 次のいずれかの文字列を指定できます。&quot;day&quot;、&quot;week&quot;、または &quot;month&quot;。 指定しない場合、既定値は &quot;day&quot; です。</p>
        <p><code>aggregationLevel</code>は、なしで<code>aggregationLevel</code>はサポートされません。 <code>aggregationLevel</code>に存在するすべての<strong>datefields</strong>に適用されます。<code>aggregationLevel</code></p>
        </td>
    </tr>
    <tr>
        <td>orderby</td>
        <td>string</td>
        <td>
            <p>各インストールの結果データ値の順序を指定するステートメントです。 構文は <code>...&orderby=field[order],field [order],...</code>です。 field パラメーターには、次のいずれかの文字列を指定できます。</p>
            <ul>
                <li>&quot;partnerTenantId&quot;</li>
                <li>&quot;id&quot;</li>
                <li>&quot;name&quot;</li>
                <li>&quot;market&quot;</li>
                <li>&quot;firstSubscriptionCreationDate&quot;</li>
                <li>&quot;latestSubscriptionCreationDate&quot;</li>
                <li>&quot;firstSubscriptionEndDate&quot;</li>
                <li>&quot;latestSubscriptionEndDate&quot;</li>
                <li>&quot;firstSubscriptionSuspendedDate&quot;</li>
                <li>&quot;latestSubscriptionSuspendedDate&quot;</li>
                <li>&quot;firstSubscriptionDeprovisionedDate&quot;</li>
                <li>&quot;latestSubscriptionDeprovisionedDate&quot;</li>
                <li>&quot;subscriptionCount&quot;</li>
                <li>&quot;licenseCount&quot;</li>
            </ul>
            <p><em>Order</em>パラメーターは省略可能で、 <code>asc</code>または<code>desc</code>にすることができます。フィールドごとに昇順または降順を指定する場合は。 既定では、 <code>asc</code>です。</p>
            <p><strong>例:</strong></br>
                <code>...&orderby=market,subscriptionCount</code>
            </p>
        </td>
    </tr>
    <tr>
        <td>groupby</td>
        <td>string</td>
        <td>
            <p>指定したフィールドのみにデータ集計を適用するステートメントです。 次のフィールドを指定できます。</p>
            <ul>
                <li><em>partnerTenantId</em></li>
                <li><em>id</em></li>
                <li><em>名前</em></li>
                <li><em>マーケティング</em></li>
                <li><em>firstSubscriptionCreationDate</em></li>
                <li><em>latestSubscriptionCreationDate</em></li>
                <li><em>firstSubscriptionEndDate</em></li>
                <li><em>latestSubscriptionEndDate</em></li>
                <li><em>firstSubscriptionSuspendedDate</em></li>
                <li><em>latestSubscriptionSuspendedDate</em></li>
                <li><em>firstSubscriptionDeprovisionedDate</em></li>
                <li><em>latestSubscriptionDeprovisionedDate</em></li>
            </ul>
            <p>返されるデータ行には、 <code>groupby</code>句で指定されたフィールドと、次のフィールドが含まれます。</p>
            <ul>
                <li><em>indirectResellerCount</em></li>
                <li><em>licenseCount</em></li>
                <li><em>subscriptionCount</em></li>
            </ul>
            <p><code>groupby</code>パラメーターは、 <code>aggregationLevel</code>パラメーターと共に使用できます。</p>
            <p><strong>例:</strong></br>
                <code>...&groupby=ageGroup,market&aggregationLevel=week</code>
            </p>
        </td>
    </tr>
</tbody>
</table>

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文に[間接リセラー](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics)リソースのコレクションが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
{
    "partnerTenantId": "AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE",
    "id": "1111111",
    "name": "RESELLER NAME",
    "market": "US",
    "firstSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "latestSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "firstSubscriptionEndDate": "2018-11-07T00:00:00",
    "latestSubscriptionEndDate": "2018-11-07T00:00:00",
    "firstSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "latestSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "firstSubscriptionDeprovisionedDate": "0001-01-01T00:00:00",
    "latestSubscriptionDeprovisionedEndDate": "0001-01-01T00:00:00",
    "subscriptionCount": 10,
    "licenseCount": 20
}
```

## <a name="see-also"></a>関連項目

- [パートナー センターの分析 - リソース](partner-center-analytics-resources.md)
