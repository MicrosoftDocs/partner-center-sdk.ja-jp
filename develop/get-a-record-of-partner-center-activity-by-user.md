---
title: パートナー センター アクティビティのレコードを取得する
description: パートナーのユーザーまたはアプリケーションが一定期間に実行した操作の記録を取得する方法。
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f5795a87db1c4d1a5ca72eb55512aacc57bb949
ms.sourcegitcommit: 529b07030a874d644cf947790f4b53cdff438dd4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "91007650"
---
# <a name="get-a-record-of-partner-center-activity"></a>パートナー センター アクティビティのレコードを取得する

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

この記事では、一定期間にパートナーのユーザーまたはアプリケーションによって実行された操作のレコードを取得する方法について説明します。

この API を使用して、現在の日付から過去30日間の監査レコードを取得します。または、開始日または終了日を含めることによって指定された日付範囲を取得します。 ただし、パフォーマンス上の理由から、アクティビティログデータの可用性は過去90日間に制限されていることに注意してください。 現在の日付より前の開始日が90日を超える要求は、無効な要求例外 (エラーコード: 400) と適切なメッセージを受け取ります。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

## <a name="c"></a>C\#

パートナーセンターの操作のレコードを取得するには、まず取得するレコードの日付範囲を設定します。 次のコード例では、開始日のみを使用しますが、終了日を含めることもできます。 詳細については、「**Query**/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) メソッド」を参照してください。 次に、適用するフィルターの種類に必要な変数を作成し、適切な値を割り当てます。 たとえば、会社名の部分文字列でフィルター処理を行うには、部分文字列を保持する変数を作成します。 顧客 ID でフィルター処理するには、ID を保持する変数を作成します。

次の例では、会社名の部分文字列、顧客 ID、またはリソースの種類でフィルター処理するサンプルコードが提供されています。 1つを選択し、他のコメントをコメントアウトします。 どちらの場合も、最初に既定の [**コンストラクター**/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) を使用して [**simplefieldfilter**/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) オブジェクトをインスタンス化し、フィルターを作成します。 次に示すように、検索するフィールドを含む文字列と、適用する適切な演算子を渡す必要があります。 また、によってフィルター処理する文字列も指定する必要があります。

次に、[**Auditrecords**/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords)] プロパティを使用してレコード操作を監査するためのインターフェイスを取得し、[**Query**/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query] または [**QueryAsync**/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) メソッドを呼び出して、フィルターを実行し、結果の最初のページを表す [**auditrecords の**/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) のコレクションを取得します。 メソッドに開始日、この例で使用されていない省略可能な終了日、およびエンティティに対するクエリを表す [**Iquery**/dotnet/api/microsoft.store.partnercenter.models.query.iquery) オブジェクトを渡します。 IQuery オブジェクトは、上記で作成したフィルターを [**Queryfactory の**/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**buildsimplequery**/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) メソッドに渡すことによって作成されます。

項目の最初のページが表示されたら、[/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create の**作成**] メソッドを使用して、残りのページを反復処理するために使用できる列挙子を作成します。

```csharp
// IAggregatePartner partnerOperations;

var startDate = new DateTime(DateTime.Now.Year, DateTime.Now.Month, 01);

// First perform the query, then get the enumerator. Choose one of the following and comment out the other two.

// To retrieve audit records by company name substring (for example "bri" matches "Fabrikam, Inc.").
var searchSubstring="bri";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CompanyName.ToString(), FieldFilterOperation.Substring, searchSubstring);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by customer ID.
var customerId="0c39d6d5-c70d-4c55-bc02-f620844f3fd1";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CustomerId.ToString(), FieldFilterOperation.Equals, customerId);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by resource type.
int resourceTypeInt = 3; // Subscription Resource.
string searchField = Enum.GetName(typeof(ResourceType), resourceTypeInt);
var filter = new SimpleFieldFilter(AuditRecordSearchField.ResourceType.ToString(), FieldFilterOperation.Equals, searchField);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

var auditRecordEnumerator = partnerOperations.Enumerators.AuditRecords.Create(auditRecordsPage);

int pageNumber = 1;
while (auditRecordEnumerator.HasValue)
{
    // Work with the current page.
    foreach (var c in auditRecordEnumerator.Current.Items)
    {
        // Display some info, such as operation type, operation date, and operation status.
        Console.WriteLine(string.Format("{0} {1} {2}.", c.OperationType, c.OperationDate, c.OperationStatus));
    }

    // Get the next page of audit records.
    auditRecordEnumerator.Next();
}
```

**サンプル**: [コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル **フォルダー**: 監査

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/V1/auditrecords? startDate = {STARTDATE} HTTP/1.1                                                                                                     |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/V1/auditrecords? startDate = {startDate} &endDate = {ENDDATE} HTTP/1.1                                                                                   |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/V1/auditrecords? startDate = {startdate} &endDate = {enddate} &filter = {"Field": "CompanyName", "Value": "{searchsubstring}", "Operator": "substring"} HTTP/1.1 |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/V1/auditrecords? startDate = {startdate} &endDate = {enddate} &filter = {"Field": "CustomerId", "Value": "{customerid}", "Operator": "equals"} HTTP/1.1          |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/V1/auditrecords? startDate = {startdate} &endDate = {enddate} &filter = {"Field": "ResourceType", "Value": "{resourcetype}", "Operator": "equals"} HTTP/1.1      |

### <a name="uri-parameter"></a>URI パラメーター

要求の作成時には、次のクエリパラメーターを使用します。

| 名前      | 種類   | 必須 | 説明                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| startDate | 日付   | いいえ       | Yyyy-mm-dd 形式の開始日。 何も指定しない場合、結果セットの既定値は、要求日の30日前になります。 フィルターが指定されている場合、このパラメーターは省略可能です。                                          |
| endDate   | 日付   | いいえ       | Yyyy-mm-dd 形式の終了日。 フィルターが指定されている場合、このパラメーターは省略可能です。 終了日を省略した場合、または null に設定した場合、要求は max ウィンドウを返します。または、今日を終了日として使用します。 |
| filter    | string | いいえ       | 適用するフィルター。 このパラメーターは、エンコードされた文字列である必要があります。 開始日または終了日が指定されている場合、このパラメーターは省略可能です。                                                                                              |

### <a name="filter-syntax"></a>フィルターの構文
フィルターパラメーターは、コンマ区切りの一連のキーと値のペアとして構成する必要があります。 各キーと値は、個別に引用符で囲まれ、コロンで区切られている必要があります。 フィルター全体はエンコードされている必要があります。

エンコードされていない場合、 のようになります。

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

次の表では、必要なキーと値のペアについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>キー</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>フィールド</td>
<td>フィルター処理するフィールド。 サポートされている値については、「 <a href="#rest-request">要求の構文</a>」を参照してください。</td>
</tr>
<tr class="even">
<td>値</td>
<td>フィルター処理される値。 値の大文字と小文字の区別は無視されます。 次の値パラメーターは、 <a href="#rest-request">要求構文</a>に示すようにサポートされています。
<ul>
<li><p>searchSubstring-会社名で置き換えます。 会社名の一部と一致する部分文字列を入力できます (たとえば、 `bri` が一致し `Fabrikam, Inc` ます)。</p>
<p>例: &quot; 値 &quot; : &quot; bri&quot;</p></li>
<li><p>customerId-顧客識別子を表す GUID 形式の文字列で置き換えます。</p>
<p>例: &quot; 値 &quot; : &quot; 0c39d6d5-c70d47 c55-bc02-f62084 4f3fd1&quot;</p></li>
<li><p>resourceType-監査レコードを取得するリソースの種類 (たとえば、Subscription) で置き換えます。 使用可能なリソースの種類は、 <a href="/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype"><strong>ResourceType</strong></a>で定義されています。</p>
<p>例: &quot; 値 &quot; : &quot; Subscription&quot;</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>演算子</td>
<td>適用する演算子。 サポートされている演算子については、「 <a href="#rest-request">要求の構文</a>」を参照してください。</td>
</tr>
</tbody>
</table>

### <a name="request-headers"></a>要求ヘッダー

- 詳細については、「 [Parter CENTER REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=6/1/2017%2012:00:00%20AM&filter=%7B%22Field%22:%22CustomerId%22,%22Value%22:%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22,%22Operator%22:%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドはフィルターに一致する一連のアクティビティを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 2859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CV: 4xDKynq/zE2im0wj.0
MS-ServerId: 030011719
Date: Tue, 27 Jun 2017 22:19:46 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "resourceType": "order",
            "resourceNewValue": "{\"Id\":\"d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"ReferenceCustomerId\":\"0c39d6d5-c70d-4c55-bc02-f620844f3fd1\",\"BillingCycle\":\"none\",\"LineItems\":[{\"LineItemNumber\":0,\"OfferId\":\"C0BD2E08-11AC-4836-BDC7-3712E744922F\",\"SubscriptionId\":\"488745B5-2086-4912-802C-6ABB9F7C3638\",\"ParentSubscriptionId\":null,\"FriendlyName\":\"Office 365 Business Premium Trial\",\"Quantity\":25,\"PartnerIdOnRecord\":null,\"Links\":{\"Subscription\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638\",\"Method\":\"GET\",\"Headers\":[]}}}],\"CreationDate\":\"2017-06-15T15:56:04.077-07:00\",\"Links\":{\"Self\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/orders/d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"Method\":\"GET\",\"Headers\":[]}},\"Attributes\":{\"Etag\":\"eyJpZCI6ImQ1MWEwNTJlLTA0M2MtNGEyYS1hYTM3LTJiYjkzOGNlZjZjMSIsInZlcnNpb24iOjF9\",\"ObjectType\":\"Order\"}}",
            "operationType": "create_order",
            "operationDate": "2017-06-15T22:56:05.0589308Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "OrderId",
                    "value": "d51a052e-043c-4a2a-aa37-2bb938cef6c1"
                }, {
                    "key": "BillingCycle",
                    "value": "None"
                }, {
                    "key": "OfferId-0",
                    "value": "C0BD2E08-11AC-4836-BDC7-3712E744922F"
                }, {
                    "key": "SubscriptionId-0",
                    "value": "488745B5-2086-4912-802C-6ABB9F7C3638"
                }, {
                    "key": "SubscriptionName-0",
                    "value": "Office 365 Business Premium Trial"
                }, {
                    "key": "Quantity-0",
                    "value": "25"
                }, {
                    "key": "PartnerOnRecord-0",
                    "value": null
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "applicationId": "Partner Center Native App",
            "resourceType": "license",
            "resourceNewValue": "{\"LicensesToAssign\":[{\"ExcludedPlans\":null,\"SkuId\":\"efccb6f7-5641-4e0e-bd10-b4976e1bf68e\"}],\"LicensesToRemove\":null,\"LicenseWarnings\":[],\"Attributes\":{\"ObjectType\":\"LicenseUpdate\"}}",
            "operationType": "update_customer_user_licenses",
            "operationDate": "2017-06-01T20:09:07.0450483Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "CustomerUserId",
                    "value": "482e2152-4b49-48ec-b715-823365ce3d4c"
                }, {
                    "key": "AddedLicenseSkuId",
                    "value": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e"
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/auditrecords?startDate=2017-06-01&size=500&filter=%7B%22Field%22%3A%22CustomerId%22%2C%22Value%22%3A%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```