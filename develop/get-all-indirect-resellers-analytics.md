---
title: Get all indirect resellers analytics information
description: How to get all the indirect resellers analytics information.
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: a13814e2e53d89e326b436bba4e134ba41c72547
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485982"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Get all indirect resellers analytics information

**Applies To**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター


How to get all the indirect resellers analytics information for your customers. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only. 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>REST Request


**Request syntax**

| メソッド  | 要求 URI |
|---------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/indirectresellers HTTP/1.1 |

 

**URI parameters**

<table>
<thead>
    <th>パラメーター</th>
    <th>タスクバーの検索ボックスに</th>
    <th>説明</th>
</thead>
<tbody>
    <tr>
        <td>partnerTenantId</td>
        <td>string</td>
        <td>The Tenant ID of the partner for which you want to retrieve indirect resellers data. </td>
    </tr>
    <tr>
        <td>id</td>
        <td>string</td>
        <td>Indirect reseller ID</td>
    </tr>
    <tr>
        <td>名前</td>
        <td>string</td>
        <td>The Name of the partner for which you want to retrieve indirect resellers data.</td>
    </tr>
    <tr>
        <td>market</td>
        <td>string</td>
        <td>The Market of the partner for which you want to retrieve indirect resellers data.</td>
    </tr>
    <tr>
        <td>firstSubscriptionCreationDate</td>
        <td>string in UTC date time format</td>
        <td>The creation date of the first subscription based on which you want to retrieve indirect resellers data.</td>
    </tr>
    <tr>
        <td>latestSubscriptionCreationDate</td>
        <td>string in UTC date time format</td>
        <td>The creation date of the latest subscription.</td>
    </tr>
    <tr>
        <td>firstSubscriptionEndDate</td>
        <td>string in UTC date time format</td>
        <td>First time any subscription was ended.</td>
    </tr>
    <tr>
        <td>latestSubscriptionEndDate</td>
        <td>string in UTC date time format</td>
        <td>Latest date when any subscription was ended. </td>
    </tr>
    <tr>
        <td>firstSubscriptionSuspendedDate</td>
        <td>string in UTC date time format</td>
        <td>First time any subscription was suspended.</td>
    </tr>
    <tr>
        <td>latestSubscriptionSuspendedDate</td>
        <td>string in UTC date time format</td>
        <td>Latest date when any subscription was suspended.</td>
    </tr>
    <tr>
        <td>firstSubscriptionDeprovisionedDate</td>
        <td>string in UTC date time format</td>
        <td>First time any subscription was deprovisioned.</td>
    </tr>
    <tr>
        <td>latestSubscriptionDeprovisionedDate</td>
        <td>string in UTC date time format</td>
        <td>Latest date when any subscription was deprovisioned.</td>
    </tr>
    <tr>
        <td>subscriptionCount</td>
        <td>double</td>
        <td>Subscription count for all value added resellers</td>
    </tr>
    <tr>
        <td>licenseCount</td>
        <td>double</td>
        <td>License count for all value added resellers</td>
    </tr>
    <tr>
        <td>indirectResellerCount</td>
        <td>double</td>
        <td>Indirect resellers count</td>
    </tr>
    <tr>
        <td>top</td>
        <td>string</td>
        <td>要求で返すデータの行数です。 指定されない場合の既定値は、最大値でもある 10000 です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。</td>
    </tr>
    <tr>
        <td>skip</td>
        <td>整数</td>
        <td>
          <p>クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 For example, <code>top=10000 and skip=0</code> retrieves the first 10000 rows of data, <code>top=10000 and skip=10000</code> retrieves the next 10000 rows of data, and so on.</p>
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
                <li><em>market</em></li>
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
        <td><p>集計データを取得する時間範囲を指定します。 次のいずれかの文字列を指定できます。&quot;day&quot;、&quot;week&quot;、または &quot;month&quot;。 指定されていない場合、既定値は &quot;day&quot; です。</p>
        <p><em>aggregationLevel</em> is not supported without a <strong>groupby</strong>. <em>aggregationLevel</em> applies to all <strong>datefields</strong> present in the <strong>groupby</strong></p>
        </td>
    </tr>
    <tr>
        <td>orderby</td>
        <td>string</td>
        <td>
            <p>各インストールの結果データ値の順序を指定するステートメントです。 The syntax is <code>...&orderby=field[order],field [order],...</code> The field parameter can be one of the following strings:</p>
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
            <p><em>order</em> パラメーターは省略可能であり、&quot;asc&quot; または &quot;desc&quot; を指定して、各フィールドを昇順または降順にすることができます。 既定値は &quot;asc&quot; です。</p>
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
                <li><em>market</em></li>
                <li><em>firstSubscriptionCreationDate</em></li>
                <li><em>latestSubscriptionCreationDate</em></li>
                <li><em>firstSubscriptionEndDate</em></li>
                <li><em>latestSubscriptionEndDate</em></li>
                <li><em>firstSubscriptionSuspendedDate</em></li>
                <li><em>latestSubscriptionSuspendedDate</em></li>
                <li><em>firstSubscriptionDeprovisionedDate</em></li>
                <li><em>latestSubscriptionDeprovisionedDate</em></li>
            </ul>
            <p>返されるデータ行には、<em>groupby</em> パラメーターに指定したフィールドと次の値が含まれます。</p>
            <ul>
                <li><em>indirectResellerCount</em></li>
                <li><em>licenseCount</em></li>
                <li><em>subscriptionCount</em></li>
            </ul>
            <p><em>groupby</em> パラメーターは、<em>aggregationLevel</em> パラメーターと同時に使用できます。</p>
            <p><strong>例:</strong></br>
                <code>...&groupby=ageGroup,market&aggregationLevel=week</code>
            </p>
        </td>
    </tr>
</tbody>
</table>
 

**Request headers**

- See [Headers](headers.md) for more information.

**Request body**

なし。

**Request example**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>Response


If successful, the response body contains a collection of [indirect resellers](partner-center-analytics-resources.md#indirect_resellers) resources.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

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


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>See also
 - [Partner Center Analytics - Resources](partner-center-analytics-resources.md)
