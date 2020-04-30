---
title: Azure に関する顧客の使用率レコードを取得する
description: Azure 使用率 API を使用して、指定した期間における顧客の Azure サブスクリプションの使用率レコードを取得できます。
ms.assetid: 0270DBEA-AAA3-46FB-B5F0-D72B9BAC3112
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 3ee3f2187f0e4961a7945c865bbcb80b90a6cf4b
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155324"
---
# <a name="get-a-customers-utilization-records-for-azure"></a>Azure に関する顧客の使用率レコードを取得する

**適用対象:**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Azure 使用率 API を使用して、指定した期間の顧客の Azure サブスクリプションの使用率レコードを取得できます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナーセンターの[ダッシュボード](https://partner.microsoft.com/dashboard)で確認できます。 パートナーセンターメニューの [ **CSP** ] を選択し、[ **Customers**] をクリックします。 [Customer] リストから顧客を選択し、[Account] \ (**アカウント**\) を選択します。 お客様のアカウントページで、[**お客様のアカウント情報**] セクションで**Microsoft ID**を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- サブスクリプション識別子。

この API は、任意の期間の日単位および時間単位の超過使用量を返します。 ただし、*この API は Azure プランではサポートされていません*。 Azure プランをお持ちの場合は、「 [invoice 未請求従量課金明細](get-invoice-unbilled-consumption-lineitems.md)書を取得する」と「[請求書の課金対象の明細項目を取得](get-invoice-billed-consumption-lineitems.md)する」を参照してください。 これらの記事では、リソースごとに1メートルあたり1日に評価された使用量を取得する方法について説明します。 このレート使用量は、Azure 使用率 API によって提供される1日の粒度のデータと同じです。 請求書の識別子を使用して、課金対象の使用状況データを取得する必要があります。 または、現在と以前の期間を使用して、未請求の使用量の推定値を取得することもできます。 *Azure プランサブスクリプションリソースでは、1時間ごとの粒度データと任意の日付範囲フィルターは現在サポートされていません*。

## <a name="azure-utilization-api"></a>Azure Utilization API

この Azure 使用率 API は、課金システムで使用率がレポートされた日時を表す期間の使用状況レコードへのアクセスを提供します。 調整ファイルの作成と計算に使用されるのと同じ使用率データへのアクセスを提供します。 ただし、課金システムの調整ファイルのロジックはありません。 同じ期間、この API から取得した結果に対して、調整ファイルの概要結果が一致するとは限りません。

たとえば、課金システムは同じ使用率データを取得し、遅延ルールを適用して、調整ファイルの内容を決定します。 請求期間が終了すると、請求期間の終了日までのすべての使用量が調整ファイルに含まれます。 請求期間内の遅延使用は、請求期間の終了後24時間以内に報告され、次の調整ファイルで考慮されます。 パートナーの請求方法に関する遅延の規則については、「 [Azure サブスクリプションの消費データを取得](https://docs.microsoft.com/previous-versions/azure/reference/mt219001(v=azure.100))する」を参照してください。

この REST API はページングされています。 応答ペイロードが1ページより大きい場合は、次のリンクに従って、使用率レコードの次のページを取得する必要があります。

## <a name="c"></a>C\#

Azure 使用率レコードを取得するには、次のようにします。

1. 顧客 ID とサブスクリプション ID を取得します。

2. 使用率レコードを含む[**Resourcecollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1)を返すには、 [**IAzureUtilizationCollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query)メソッドを呼び出します。

3. 使用率ページを走査するための Azure 使用率レコード列挙子を取得します。 リソースコレクションがページングされているため、この手順は必須です。

- **サンプル**:[コンソールテストアプリ](console-test-app.md)
- **プロジェクト**: パートナーセンター SDK のサンプル
- **クラス**: GetAzureSubscriptionUtilization.cs

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Azure 使用率レコードを取得するには、まず顧客 id とサブスクリプション識別子が必要です。 次に、 **IAzureUtilizationCollection**関数を呼び出して、使用率レコードを含む**resourcecollection**を返します。 リソース コレクションはページングされているため、使用率ページをスキャンするには Azure 使用率レコード列挙子を取得する必要があります。

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Azure 使用率レコードを取得するには、まず顧客 id とサブスクリプション識別子が必要です。 次に、[**取得パートナーの Subscription使用率**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md)を呼び出します。 このコマンドは、指定された期間に利用可能なすべてのレコードを返します。

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法 | 要求 URI |
|------- | ----------- |
| **GET** | *{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure? 開始\_時間 = {開始時刻} &終了\_時刻 = {終了時刻} &粒度 = {粒度} &詳細\_を表示 = {True} |

#### <a name="uri-parameters"></a>URI パラメーター

使用率レコードを取得するには、次のパスとクエリパラメーターを使用します。

| 名前 | Type | 必須 | 説明 |
| ---- | ---- | -------- | ----------- |
| customer-tenant-id | string | はい | 顧客を識別する GUID 形式の文字列。 |
| subscription-id | string | はい | サブスクリプションを識別する GUID 形式の文字列。 |
| start_time | UTC 日時オフセット形式の文字列 | はい | 課金システムで使用率がレポートされた日時を表す時間範囲の開始。 |
| end_time | UTC 日時オフセット形式の文字列 | はい | 課金システムで使用率がレポートされた日時を表す時間範囲の最後。 |
| 粒度 (granularity) | string | いいえ | 使用状況の集計の粒度を定義します。 使用可能なオプション`daily`は、(既定`hourly`値) とです。
| show_details | boolean | いいえ | インスタンス レベルの使用状況の詳細を取得するかどうかを指定します。 既定では、 `true`です。 |
| size | number | いいえ | 1 回の API 呼び出しで返される集計の数を指定します。 既定値は 1000 です。 最大値は1000です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし

### <a name="request-example"></a>要求の例

次の要求例では、調整ファイルが期間 7/2-8/1 に対してどのように表示されるかに似た結果が生成されます。 これらの結果は正確に一致しない場合があります (詳細については、「 [Azure 使用状況 API](#azure-utilization-api) 」セクションを参照してください)。

この要求例では、請求7/2 システムで報告された使用率 (午前12時 (UTC)) と 8/2 (午前12時 (UTC))) を返します。

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは、応答本文で[Azure 使用率レコード](azure-utilization-record-resources.md)リソースのコレクションを返します。 Azure 使用率データが依存システムでまだ準備されていない場合、このメソッドは再試行ヘッダーを含む HTTP 状態コード204を返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 ネットワークトレースツールを使用して、HTTP 状態コード、[エラーコードの種類](error-codes.md)、およびその他のパラメーターを読み取ります。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
