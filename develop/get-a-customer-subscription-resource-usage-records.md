---
title: リソース別のサブスクリプションの使用状況データの取得
description: ResourceUsageRecord リソースを使用して、現在の請求期間中に特定の Azure サービスまたはリソースの顧客のリソース使用状況レコードを取得できます。
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: af1a30a22831813f2c3b57a9500740ff606e583d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487692"
---
# <a name="get-usage-data-for-subscription-by-resource"></a>リソース別のサブスクリプションの使用状況データの取得

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

このトピックでは、 **ResourceUsageRecord**リソースを取得する方法について説明します。 このリソースは、Azure プランにプロビジョニングされた個々のリソースの月の合計を表します。 このリソースを使用して、現在の請求期間中に特定の Azure サービスまたはリソースの顧客のリソース使用状況レコードを取得できます。 この API は、Azure の Api では使用できなかったデータを返します。

*このルートは、Microsoft Azure (0145P) サブスクリプションをサポートしていません。*

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。
- 顧客識別子 (**顧客-テナント id**)。 顧客の識別子がない場合は、顧客 リストから顧客を選択し、**アカウント** を選択して、 **Microsoft ID**を保存することで、パートナーセンターで識別子を検索できます。
- サブスクリプション識別子

## <a name="c"></a>C\#

現在の請求期間中に特定の Azure サービスまたはリソースの顧客のリソース使用状況レコードを取得するには、次のようにします。

1. **Iaggregatepartner.customers**コレクションを使用して、 **ById ()** メソッドを呼び出します。
2. サブスクリプションプロパティ、 **UsageRecords**、 **Resources**プロパティの順に呼び出します。 Get () または GetAsync () メソッドを呼び出して終了します。

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

例については、以下を参照してください。

- サンプル:[コンソールテストアプリ](console-test-app.md)
- プロジェクト: **Partnersdk. FeatureSamples**
- クラス: **GetSubscriptionUsageRecordsByResource.cs**

## <a name="rest"></a>休息

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求の構文

| メソッド  | 要求 URI                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1 |

##### <a name="uri-parameters"></a>URI パラメーター

次の表に、顧客の評価された使用状況情報を取得するために必要なクエリパラメーターを示します。

| 名前                   | 種類     | 必須 | 説明                               |
|------------------------|----------|----------|-------------------------------------------|
| **顧客-テナント id** | **guid** | Y        | 顧客に対応する GUID。     |
| **サブスクリプション id**    | **guid** | Y        | パートナーセンターの[サブスクリプションリソース](subscription-resources.md#subscription)の識別子に対応する GUID。これは、Microsoft Azure (0145P) サブスクリプションまたは Azure プランを表します。 *Azure プランのサブスクリプションリソースについては、このルートの**サブスクリプション id**として**プラン id**を指定します。* |

#### <a name="request-headers"></a>要求ヘッダー

詳細については、「[ヘッダー](headers.md)」を参照してください。

#### <a name="request-body"></a>要求本文

なし。

#### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

### <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で**PagedResourceCollection\<ResourceUsageRecord >** リソースを返します。

#### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、および追加のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

#### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlement-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
