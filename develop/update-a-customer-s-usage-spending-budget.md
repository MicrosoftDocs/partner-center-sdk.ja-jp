---
title: 顧客の使用支出予算を更新する
description: 顧客の使用に割り当てられている支出予算を更新します。
ms.date: 02/05/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aa33c15031132024a6a89a36ca0ce1c45a9b0840
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095615"
---
# <a name="update-a-customers-usage-spending-budget"></a>顧客の使用支出予算を更新する

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

顧客の使用に割り当てられている[支出予算](customer-usage-resources.md#customerusagesummary)を更新します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="c"></a>C\#

顧客の使用量予算を更新するには、最初に更新された金額を含む新しい[**SpendingBudget**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget)オブジェクトを作成します。 次に、 [**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection)コレクションを使用し、指定された顧客の ID を使用して[**ById ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出します。 次に、[使用量の[**予算**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget)] プロパティにアクセスして、更新された使用量の予算を[**Patch ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch)メソッドまたは Patch [**async ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync)メソッドに渡します。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Patch(newUsageBudget);
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法    | 要求 URI                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを使用して、課金プロファイルを更新します。

| 名前                   | Type     | 必須 | 説明                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | この値は、リセラーがリセラーに属する特定の顧客の結果をフィルター処理できるようにする GUID 形式の**顧客テナント id**です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

完全なリソース。

### <a name="request-example"></a>要求の例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
     "Amount": 100,
     "Attributes": {
          "ObjectType": "SpendingBudget"
     }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは、更新された金額を持つユーザーの支出予算を返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    {
        "amount": 100,
        "usageSpendingBudget": 100,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/usagebudget",
            "method":"PATCH",
            "headers":[]
        }
    }
}
```
