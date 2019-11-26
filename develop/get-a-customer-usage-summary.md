---
title: すべての顧客のサブスクリプションの使用状況の概要を取得する
description: CustomerUsageSummary リソースを使用して、現在の請求期間中に特定の Azure サービスまたはリソースの顧客の使用状況を取得できます。
ms.assetid: 58FA3CBD-27CF-46C5-9EB2-188D83896F7D
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 5733773e011701d13ce5aee5bbcd37417dfedaab
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487662"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a>すべての顧客のサブスクリプションの使用状況の概要を取得する

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**CustomerUsageSummary**リソースを使用して、現在の請求期間中に特定の Azure サービスまたはリソースの顧客の使用状況を取得できます。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。
- 顧客識別子 (**顧客-テナント id**)。 顧客の識別子がない場合は、顧客 リストから顧客を選択し、**アカウント** を選択して、 **Microsoft ID**を保存することで、パートナーセンターで識別子を検索できます。

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

- サンプル:[コンソールテストアプリ](console-test-app.md)
- プロジェクト: **Partnersdk. FeatureSamples**
- クラス: **GetCustomerUsageSummary.cs**

## <a name="rest"></a>休息

### <a name="rest-request"></a>REST 要求

#### <a name="request-syntax"></a>要求の構文

| メソッド  | 要求 URI                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| **取得** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1 |

##### <a name="uri-parameter"></a>URI パラメーター

次の表に、顧客の評価された使用状況情報を取得するために必要なクエリパラメーターを示します。

| 名前                   | 種類     | 必須 | 説明                           |
|------------------------|----------|----------|---------------------------------------|
| **顧客-テナント id** | **guid** | Y        | 顧客に対応する GUID。 |

#### <a name="request-headers"></a>要求ヘッダー

詳細については、「[ヘッダー](headers.md) 」を参照してください。

#### <a name="request-body"></a>要求本文

なし。

#### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

### <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で**CustomerUsageSummary**リソースを返します。

#### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、および追加のパラメーターを読み取ります。 完全な一覧については、「[エラーコード](error-codes.md)」を参照してください。

#### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a>Microsoft Azure (0145P) サブスクリプションの応答の例

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

#### <a name="response-example-for-azure-plan"></a>Azure プランの応答の例

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
