---
title: サブスクリプションの毎月の使用状況レコードをすべて取得します。
description: AzureResourceMonthlyUsageRecord リソースコレクションを使用すると、顧客のサブスクリプション内のサービスの一覧と、それらに関連付けられた評価済みの使用状況情報を取得できます。
ms.assetid: 037D71B9-8E8B-4BC0-8388-9CBC97218CED
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0acd284c1b829330283d2012fcb6a85d3553f763
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485972"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a>サブスクリプションの毎月の使用状況レコードをすべて取得します。

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

[**AzureResourceMonthlyUsageRecord**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord)リソースコレクションを使用すると、顧客のサブスクリプション内のサービスの一覧と、それらに関連付けられた評価済みの使用状況情報を取得できます。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客識別子 (**顧客-テナント id**)。 顧客の識別子がない場合は、顧客 リストから顧客を選択し、**アカウント** を選択して、 **Microsoft ID**を保存することで、パートナーセンターで識別子を検索できます。
- サブスクリプション識別子。

*この API は、Microsoft Azure (0145P) サブスクリプションのみをサポートしています。Azure プランを使用している場合は、「[測定によるサブスクリプションの使用状況データの取得](get-a-customer-subscription-meter-usage-records.md)」を参照してください。*

## <a name="c"></a>C\#

サブスクリプションのリソース使用状況に関する情報を取得するには、次のようにします。

1. **Iaggregatepartner.customers**コレクションを使用して、 **ById ()** メソッドを呼び出します。 
2. **サブスクリプション**プロパティ、 **UsageRecords**、 **Resources**プロパティの順に呼び出します。 
3. **Get ()** または**GetAsync ()** メソッドを呼び出します。

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

例については、以下を参照してください。

- サンプル:[コンソールテストアプリ](console-test-app.md)
- プロジェクト: **Partnersdk. FeatureSample**
- クラス: **SubscriptionResourceUsageRecords.cs**

## <a name="rest"></a>休息

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求の構文

| メソッド  | 要求 URI                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1 |

##### <a name="uri-parameters"></a>URI パラメーター

次の表に、評価された使用状況情報を取得するために必要なクエリパラメーターを示します。

| 名前                    | 種類     | 必須 | 説明                               |
|-------------------------|----------|----------|-------------------------------------------|
| **顧客-テナント id**  | **guid** | Y        | 顧客に対応する GUID。     |
| **サブスクリプション id** | **guid** | Y        | サブスクリプションに対応する GUID。 |

#### <a name="request-headers"></a>要求ヘッダー

詳細については、「[ヘッダー](headers.md)」を参照してください。

#### <a name="request-body"></a>要求本文

なし。

#### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

### <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で**AzureResourceMonthlyUsageRecord**リソースのコレクションを返します。

#### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

#### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 648a26a4-a63e-459f-844b-4f29d7913353
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    "totalCount":20,
    "items":[{
        "category":"Storage",
        "subcategory":"LOCALLY REDUNDANT",
        "quantityUsed":0.151287527825352,
        "unit":"GB",
        "id":"2a2419c0-cefe-46b2-8004-8eb002ad606c",
        "name":"Azure Resource 1",
        "totalCost":0.195779159290613,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    },
    {
        "category":"Remote App",
        "subcategory":"Remote App",
        "quantityUsed":0.932546524299563,
        "unit":"GB",
        "id":"7e4099c8-2b3d-41a6-a1bd-d5cf315989b2",
        "name":"Azure Resource 2",
        "totalCost":0.920983775016379,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    }],
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>%20/usagerecords",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
