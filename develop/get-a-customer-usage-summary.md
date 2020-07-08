---
title: すべての顧客のサブスクリプションの使用状況の概要を取得する
description: CustomerUsageSummary リソースを使用して、現在の請求期間中に特定の Azure サービスまたはリソースの顧客の使用状況を取得できます。
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c918434367a3514e6a6ad6034b4897c33f51025
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098232"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a>すべての顧客のサブスクリプションの使用状況の概要を取得する

**適用対象:**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**CustomerUsageSummary**リソースを使用して、現在の請求期間中に特定の Azure サービスまたはリソースの顧客の使用状況を取得できます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="c"></a>C\#

すべての顧客のサブスクリプションの使用状況の概要を取得するには、次のようにします。

1. **Iaggregatepartner.customers**コレクションを使用して、 **ById ()** メソッドを呼び出します。

2. **UsageSummary**プロパティを呼び出した後、 **Get ()** または**GetAsync ()** の各メソッドを呼び出します。

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

例については、以下を参照してください。

- サンプル: [コンソール テスト アプリ](console-test-app.md)
- プロジェクト: **Partnersdk. FeatureSamples**
- クラス: **GetCustomerUsageSummary.cs**

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

次の表に、顧客の評価された使用状況情報を取得するために必要なクエリパラメーターを示します。

| 名前                   | Type     | 必須 | 説明                           |
|------------------------|----------|----------|---------------------------------------|
| **customer-tenant-id** | **guid** | Y        | 顧客に対応する GUID。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で**CustomerUsageSummary**リソースを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a>Microsoft Azure (0145P) サブスクリプションの応答の例

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
    "budget":{
        "ammount":300.000000,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "id":"65726577-C208-40FD-9735-8C85AC9CAC68",
    "name":"600 test",
    "billingStartDate":"2016-02-06T00:00:00-08:00",
    "billingEndDate":"2016-03-05T00:00:00-08:00",
    "totalCost":0.0,
    "currencyLocale":"en-US",
    "lastModifiedDate":"2016-02-26T09:42:54.5130558+00:00",
    "links":{
        "self":{
            "uri":"/customers/{customer-tenant-id}/usagesummary",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"CustomerUsageSummary"
    }
}
```

### <a name="response-example-for-azure-plan"></a>Azure プランの応答の例

この例では、顧客が Azure プランを購入しています。

*Azure プランをご利用のお客様には、API の応答に次のような変更が加えられています。*

- **currencyLocale**は**currencyCode**に置き換えられます。
- **usdTotalCost**は新しいフィールドです。

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget": {
        "amount": 97,
        "attributes": {
            "objectType": "SpendingBudget"
        }
    },
    "resourceId": "44908a11-641b-4c53-b7fc-0f2bfca8a581",
    "resourceName": "Modern Azure Customer UK",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "attributes": {
        "objectType": "CustomerUsageSummary"
    }
}
```
