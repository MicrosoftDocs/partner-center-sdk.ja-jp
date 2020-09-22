---
title: 顧客との再販業者関係の削除
description: 取引がなくなった顧客との再販業者関係を削除する方法。
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 786dbeef91e51b2f7830a6d49e47e29121a7c38b
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926784"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>顧客との再販業者関係の削除

**適用対象**

- パートナー センター

取引がなくなった顧客との再販業者関係を削除します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- すべての Azure 予約 VM インスタンスの注文は、再販業者の関係を削除する前にキャンセルする必要があります。 開いている Azure 予約 VM インスタンスの注文を取り消すには、Azure サポートにお問い合わせください。

## <a name="c"></a>C\#

顧客の再販業者関係を削除するには、まず、その顧客のアクティブな Azure Reserved VM Instances がキャンセルされていることを確認します。 次に、その顧客のすべてのアクティブなサブスクリプションが中断されていることを確認します。 これを行うには、再販業者の関係を削除する顧客の ID を決定します。 次のコード例では、ユーザーは顧客識別子を入力するように求められます。

顧客の Azure Reserved VM Instances を取り消す必要があるかどうかを判断するには、顧客の識別子を使用して [**iaggregatepartner.customers. ById**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) メソッドを呼び出し、権利のコレクション操作へのインターフェイスを取得するための [**権利**/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions] プロパティを呼び出して、権利のコレクションを取得します。 権利コレクションを取得するには、[**Get**/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) または [**GetAsync**/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) メソッドを呼び出します。 EntitlementType の [**EntitlementType**](entitlement-resources.md#entitlementtype) 値を持つ権利のコレクションをフィルター処理し [**ます。 VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) がある場合は、続行する前にサポートを呼び出して取り消します。

次に、顧客の識別子を使用して [**iaggregatepartner.customers. ById**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) メソッドを呼び出して顧客を指定し、[**subscription/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions]** プロパティを呼び出してサブスクリプションコレクション操作へのインターフェイスを取得することによって、顧客のサブスクリプションのコレクションを取得します。 最後に、[**Get**/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get)] または [**GetAsync**/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync] メソッドを呼び出して、顧客のサブスクリプションコレクションを取得します。 サブスクリプションコレクションを走査し、サブスクリプションのいずれにも **[/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status]** プロパティの値が [**Subscriptionstatus. Active**/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus) でないことを確認します。 サブスクリプションがアクティブな場合は、中断する方法については、「 [サブスクリプションを中断](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) する」を参照してください。

その顧客のすべてのアクティブな Azure Reserved VM Instances が取り消され、すべてのアクティブなサブスクリプションが中断されていることを確認したら、その顧客の再販業者の関係を削除できます。 最初に、新しい [Customer/dotnet/api//dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship) オブジェクトを作成します。このオブジェクトには、[dotnet/api/] プロパティが [] に設定されています。このオブジェクトは、**"**" に設定されています。このオブジェクトは、 次に、顧客識別子を使用して顧客を指定するために、[**iaggregatepartner.customers. ById**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) メソッドを呼び出し、 **Patch** メソッドを呼び出して、新しい customer オブジェクトを渡します。

関係を再確立するには、[再販業者の関係/パートナー-センター/開発/要求-再販業者-関係を要求する] のプロセスを繰り返します。

``` csharp
// IAggregatePartner partnerOperations;

// Prompt the user the enter the customer ID.
var customerIdToDeleteRelationshipOf = this.Context.ConsoleHelper.ReadNonEmptyString("Please enter the ID of the customer you want to delete the relationship with", "The customer ID can't be empty");

// Determine if there are any active Azure Reserved VM Instances for this customer.
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Entitlements.Get();

If (entitlements.Items.Where(x => x.EntitlementType == EntitlementType.VirtualMachineReservedInstance).Any())
{
    this.Context.ConsoleHelper.Warning("Please cancel Azure Reserved Virtual Machine Instance orders through support and try again. Aborting the delete customer relationship operation");
               return;
}

// Verify that there are no active subscriptions.
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Subscriptions.Get();
IList<Subscription> subscriptions = new List<Subscription>(customerSubscriptions.Items);

foreach (Subscription customerSubscription in subscriptions)
{
    if (customerSubscription.Status == SubscriptionStatus.Active)
    {
        this.Context.ConsoleHelper.Warning(String.Format("Subscription with ID :{0}  OfferName: {1} cannot be in active state, ", customerSubscription.Id, customerSubscription.OfferName));
        this.Context.ConsoleHelper.Warning("Please Suspend all the Subscriptions and try again. Aborting the delete customer relationship operation");
               return;
    }
}

// Delete the customer's relationship to the partner.
Customer customer = new Customer();
customer.RelationshipToPartner = CustomerPartnerRelationship.None;
customer = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Patch(customer);

if (customer.RelationshipToPartner == CustomerPartnerRelationship.None)
{
    this.Context.ConsoleHelper.Success("Customer Partner Relationship successfully deleted");
}
```

**サンプル**: [コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: partnersdk. FeatureSample **クラス**: DeletePartnerCustomerRelationship.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法     | 要求 URI                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **PATCH**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次の表に、リセラー関係を削除するために必要なクエリパラメーターを示します。

| 名前                   | 種類     | 必須 | 説明                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | この値は、顧客を識別する GUID 形式の **顧客テナント id** です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

要求本文には、 **顧客** リソースが必要です。 **Relationshiptopartner**プロパティが [なし] に設定されていることを確認します。

### <a name="request-example"></a>要求の例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Content-Length: 74
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
MS-RequestId: 9fef8b23-6e3e-45d2-8678-e9fe89c35af5
Date: Fri, 12 Jan 2018 00:31:55 GMT

{
    "relationshipToPartner":"none",
    "attributes":{
        "objectType":"Customer"
    }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは、指定された顧客の再販業者の関係を削除します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
MS-RequestId: 7988dde4-b516-472c-b226-6d53fb18f04e
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
X-Locale: en-US
Content-Type: application/json
Content-Length: 242
Expect: 100-continue

{
    "Id":null,
    "CommerceId":null,
    "CompanyProfile":null,
    "BillingProfile":null,
    "RelationshipToPartner":"none",
    "AllowDelegatedAccess":null,
    "UserCredentials":null,
    "CustomDomains":null,
    "AssociatedPartnerId":null,
    "Attributes":{
        "ObjectType":"Customer"
    }
}
```
