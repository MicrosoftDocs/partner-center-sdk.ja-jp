---
title: 顧客のサブスクリプションの使用状況の概要を取得する
description: SubscriptionUsageSummary リソースを使用して、現在の請求期間中に特定の Azure サービスまたはリソースのサブスクリプション使用状況の概要を取得できます。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30334b6f08829eccf0693b566c11f94cb3ece976
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098245"
---
# <a name="get-usage-summary-for-customers-subscription"></a>顧客のサブスクリプションの使用状況の概要を取得する

**適用対象:**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**SubscriptionUsageSummary**リソースを使用して、顧客のサブスクリプションの使用状況の概要を取得できます。 このリソースは、現在の請求期間中に特定の Azure サービスまたはリソースのサブスクリプション使用状況の概要を表します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- サブスクリプション識別子

## <a name="c"></a>C\#

顧客のサブスクリプションのサブスクリプション使用状況の概要を取得するには、次のようにします。

1. **Iaggregatepartner.customers**コレクションを使用して、 **ById ()** メソッドを呼び出します。

2. 次に、 **UsageSummary**プロパティと同様に、サブスクリプションプロパティを呼び出します。 Get () または GetAsync () メソッドを呼び出して終了します。

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

例については、以下を参照してください。

- サンプル: [コンソール テスト アプリ](console-test-app.md)
- プロジェクト: **Partnersdk. FeatureSamples**
- クラス: **GetSubscriptionUsageSummary.cs**

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

次の表に、顧客の評価された使用状況情報を取得するために必要なクエリパラメーターを示します。

| 名前                   | Type     | 必須 | 説明                               |
|------------------------|----------|----------|-------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | 顧客に対応する GUID。     |
| **サブスクリプション id**    | **guid** | Y        | サブスクリプションの識別子に対応する GUID。 Azure プランの場合、これは、Azure プランを表す、対応するパートナーセンターの[サブスクリプションリソース](subscription-resources.md#subscription)の識別子です。 *Azure プランのサブスクリプションリソースについては、このルートの**サブスクリプション id**として**プラン id**を指定します。* |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で**SubscriptionUsageSummary**リソースを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure (0145P) サブスクリプションの応答の例

この例では、顧客が**145P Azure PayG**プランを購入しています。

*Microsoft Azure (0145P) サブスクリプションをお持ちのお客様については、API 応答に変更はありません。*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "id": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "resourceName": "Microsoft Azure",
    "name": "Microsoft Azure",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a>Azure プランの REST 応答の例

この例では、顧客が Azure プランを購入しています。

*Azure プランをご利用のお客様には、次の API 応答が変更されています。*

- **currencyLocale**は**currencyCode**に置き換えられます。
- **usdTotalCost**は新しいフィールドです。

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac1
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "11111111-dca5-6f31-d3a6-dbbfad9be0fc",
    "resourceName": "Azure plan",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```
