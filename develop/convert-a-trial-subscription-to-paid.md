---
title: 試用版サブスクリプションを有料版に変換する
description: 試用版のサブスクリプションを有料のサブスクリプションに変換する方法。
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ac7b6c20c71e8af0e5cbd796aa4466056d780ce9
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096351"
---
# <a name="convert-a-trial-subscription-to-paid"></a>試用版サブスクリプションを有料版に変換する

**適用対象:**

- パートナー センター

試用版のサブスクリプションを有料に変換することができます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- アクティブな試用版サブスクリプションのサブスクリプション ID。

- 使用可能な変換プラン。

## <a name="convert-a-trial-subscription-to-paid-through-code"></a>試用版サブスクリプションをコードによって有料に変換する

試用版のサブスクリプションを有料のサブスクリプションに変換するには、最初に使用可能な試用変換のコレクションを取得する必要があります。 次に、購入する変換プランを選択する必要があります。

変換プランでは、既定で試用版のサブスクリプションと同じ数のライセンスを持つ数量が指定されます。 この数量を変更するには、 [**quantity**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity)プロパティに購入するライセンス数を設定します。

> [!NOTE]
> 購入したライセンスの数に関係なく、購入したライセンスについては試用版のサブスクリプション ID が再利用されます。 結果として、有効な評価版は消え、購入によって置き換えられます。

コードを使用して試用版のサブスクリプションを変換するには、次の手順に従います。

1. 利用可能なサブスクリプション操作へのインターフェイスを取得します。 顧客を特定し、試用版サブスクリプションのサブスクリプション識別子を指定する必要があります。

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. 使用可能な変換プランのコレクションを取得します。 このメソッドの要求/応答の詳細と詳細については、「[評価版変換プランの一覧を取得する](get-a-list-of-trial-conversion-offers.md)」を参照してください。

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. 変換プランを選択します。 次のコードは、コレクション内の最初の変換プランを選択します。

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. 必要に応じて、購入するライセンス数を指定します。 既定値は、試用版サブスクリプションのライセンス数です。

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create)または[**createasync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync)メソッドを呼び出して、試用版サブスクリプションを有料に変換します。

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>C\#

試用版のサブスクリプションを有料のサブスクリプションに変換するには、次のようにします。

1. 顧客 ID を指定して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを使用し、顧客を識別します。

2. 試用版サブスクリプション ID を使用して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid)メソッドを呼び出すことにより、サブスクリプション操作へのインターフェイスを取得します。 サブスクリプション操作インターフェイスへの参照をローカル変数に保存します。

3. 変換に対して使用可能な操作へのインターフェイスを取得し、 [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get)または[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync)メソッドを呼び出して、使用可能な[**変換**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion)の提供のコレクションを取得するには、[**変換**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions)プロパティを使用します。 1つを選択する必要があります。 次の例では、使用可能な最初の変換が既定値に設定されています。

4. ローカル変数に保存したサブスクリプション操作インターフェイスへの参照と[**変換**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions)プロパティを使用して、変換で使用可能な操作へのインターフェイスを取得します。

5. 選択した変換オファーオブジェクトを[**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create)または[**createasync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync)メソッドに渡して、試用変換を試行します。

### <a name="c-example"></a>C の \# 例

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get subscription operations for the trial subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the available conversions.
var conversions = subscriptionOperations.Conversions.Get();

// If there are no conversions available, we&#39;re done.
// Otherwise, convert the trial to the first available conversion offer.
if (conversions.TotalCount <= 0)
{
    System.Console.WriteLine("This subscription has no conversions");
}
else
{
    // Default to the first conversion.
    var selectedConversion = conversions.Items.ToList()[0];

    // Convert the trial and return the result.
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
}
```

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法   | 要求 URI                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次のパスパラメーターを使用して、顧客と試用版のサブスクリプションを識別します。

| 名前            | Type   | 必須 | 説明                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| customer-id     | string | はい      | 顧客を識別する GUID 形式の文字列。           |
| subscription-id | string | はい      | 評価版サブスクリプションを識別する GUID 形式の文字列。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

設定された[変換](conversions-resources.md#conversion)リソースが要求本文に含まれている必要があります。

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 234
Expect: 100-continue

{
    "OfferId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "TargetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "OrderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
    "Quantity": 25,
    "BillingCycle": "monthly",
    "Attributes": {
        "ObjectType": "Conversion"
    }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[ConversionResult](conversions-resources.md#conversionresult)リソースが含まれます。

#### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターのエラーコード](error-codes.md)」を参照してください。

#### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 211
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CV: kW4GzmhvHEqCq1ls.0
MS-ServerId: 030020643
Date: Thu, 15 Jun 2017 23:10:40 GMT

 {
    "subscriptionId": "488745B5-2086-4912-802C-6ABB9F7C3638",
    "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "attributes": {
        "objectType": "ConversionResult"
    }
}
```
