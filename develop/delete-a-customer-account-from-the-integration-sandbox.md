---
title: 統合サンドボックスから顧客アカウントを削除する
description: 「運用環境でのテスト (Tip)」統合サンドボックスから顧客アカウントを削除する方法。
ms.assetid: B95431F6-EA7F-4C21-835F-6D6C303B05A5
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d81341f46d9131ac19ba5ae48e424423b4b761e5
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155444"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a>統合サンドボックスから顧客アカウントを削除する

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

この記事では、「運用環境でのテスト (Tip)」統合サンドボックスから顧客アカウントを削除する方法について説明します。

> [!IMPORTANT]
> 顧客アカウントを削除すると、その顧客テナントに関連付けられているすべてのリソースが削除されます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナーセンターの[ダッシュボード](https://partner.microsoft.com/dashboard)で確認できます。 パートナーセンターメニューの [ **CSP** ] を選択し、[ **Customers**] をクリックします。 [Customer] リストから顧客を選択し、[Account] \ (**アカウント**\) を選択します。 お客様のアカウントページで、[**お客様のアカウント情報**] セクションで**Microsoft ID**を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- Tip 統合サンドボックスから顧客を削除する前に、Azure Reserved Virtual Machine Instances とソフトウェアのすべての注文書をキャンセルする必要があります。

## <a name="c"></a>C\#

Tip 統合サンドボックスから顧客を削除するには、次のようにします。

1. ヒントアカウントの資格情報を[**Createpartneroperations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.partnerservice.instance)メソッドに渡して、パートナー操作への[**ipartner**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner)インターフェイスを取得します。

2. 次のように、パートナー操作インターフェイスを使用して、権利のコレクションを取得します。

    1. 顧客識別子を使用して[**ById ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出し、顧客を指定します。

    2. **権利**プロパティを呼び出します。

    3. **Get**または**GetAsync**メソッドを呼び出して、[**権利**](entitlement-resources.md)コレクションを取得します。

3. その顧客に対するすべての Azure Reserved Virtual Machine Instances とソフトウェアの注文書が取り消されていることを確認します。 コレクション内の[**権利**](entitlement-resources.md)ごとに、次のようにします。

    1. 権利を使用[**します。ReferenceOrder.Id**](entitlement-resources.md#referenceorder)は、顧客の注文のコレクションから、対応する[注文](order-resources.md#order)のローカルコピーを取得します。

    2. [ [**Order. Status**](order-resources.md#order) ] プロパティを [取り消し済み] に設定します。

    3. **Patch ()** メソッドを使用して、順序を更新します。

4. すべての注文を取り消します。 たとえば、次のコードサンプルでは、ループを使用して、その状態が "取り消されました" になるまで各注文をポーリングします。

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be cancelled.
    ResourceCollection<Entitlement> entitlements = tipAccountPartnerOperations.Customers.ById(customerTenantId).Entitlements.Get();

    // Cancel all orders
    foreach (var entitlement in entitlements)
    {
        var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
        order.Status = "Cancelled";
        order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(order.Id).Patch(order);
    }

    // Keep polling until the status of all orders is "Cancelled".
    bool proceed = true;
    do
    {
        // Check if all the orders were cancelled.
        foreach (var entitlement in entitlements)
        {
            var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
            if (!order.Status.Equals("Cancelled", StringComparison.OrdinalIgnoreCase))
            {
                proceed = false;
            }
        }

        // Wait for a few seconds.
        Thread.Sleep(5000);
    }
    while (proceed == false);

    tipAccountPartnerOperations.Customers.ById(customerTenantId).Delete();
    ```

5. 顧客の**Delete**メソッドを呼び出して、すべての注文がキャンセルされていることを確認します。

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンターの Partnercenter sdk. のサンプル**クラス**: DeleteCustomerFromTipAccount.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法     | 要求 URI                                                                            |
|------------|----------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

顧客を削除するには、次のクエリパラメーターを使用します。

| 名前                   | Type     | 必須 | 説明                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| customer-tenant-id     | GUID     | Y        | この値は、リセラーがリセラーに属する特定の顧客の結果をフィルター処理できるようにする GUID 形式の**顧客テナント id**です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし。

### <a name="request-example"></a>要求の例

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは空の応答を返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
