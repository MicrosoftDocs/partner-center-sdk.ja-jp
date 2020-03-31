---
title: 顧客との再販業者関係の削除
description: 取引がなくなった顧客との再販業者関係を削除する方法。
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 3e64b6b9921e500d4f4926a45a624c909988ec00
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415478"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>顧客との再販業者関係の削除


**適用対象**

- Partner Center  


取引がなくなった顧客との再販業者関係を削除します。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。
- 顧客 ID (顧客-テナント id)。 顧客の ID を持っていない場合は、[顧客] リストから顧客を選択し、[アカウント] を選択して、Microsoft ID を保存することで、パートナーセンターで ID を検索できます。
- すべての Azure 予約 VM インスタンスの注文は、再販業者の関係を削除する前にキャンセルする必要があります。 開いている Azure 予約 VM インスタンスの注文をキャンセルするには、Azure サポートにお問い合わせください。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


顧客の再販業者関係を削除するには、まずその顧客のアクティブな Azure Reserved VM Instances が取り消され、その顧客のすべてのアクティブなサブスクリプションが中断されていることを確認する必要があります。 これを行うには、再販業者の関係を削除する顧客の ID を決定します (次のコード例では、ユーザーは顧客 id を入力するように求められます)。 

顧客の Azure Reserved VM Instances を取り消す必要があるかどうかを判断するには、顧客を指定するために顧客識別子を使用して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出し、権利コレクション操作へのインターフェイスを取得する[**権利**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)プロパティを使用して、権利のコレクションを取得します。 [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get)または[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync)メソッドを呼び出して、権利コレクションを取得します。 EntitlementType の[**EntitlementType**](entitlement-resources.md#entitlementtype)値を持つ権利のコレクションをフィルター処理し[**ます。 VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype)がある場合は、続行する前にサポートを呼び出して取り消します。 

次に、顧客の識別子を使用して[**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出して顧客のサブスクリプションのコレクションを取得し、 [**subscription プロパティを呼び出して、サブスクリプション**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)コレクション操作へのインターフェイスを取得します。 最後に、 [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get)または[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync)メソッドを呼び出して、顧客のサブスクリプションコレクションを取得します。 サブスクリプションコレクションを走査し、サブスクリプションにサブスクリプションがないことを確認し[**ます。 Status**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status)プロパティの値は[**Subscriptionstatus. Active**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)です。 サブスクリプションがアクティブな場合は、中断する方法については、「[サブスクリプションを中断](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription)する」を参照してください。 

その顧客のすべてのアクティブな Azure Reserved VM Instances が取り消され、すべてのアクティブなサブスクリプションが中断されていることを確認したら、その顧客の再販業者の関係を削除できます。 最初に、 [customer. RelationshipToPartner](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner)プロパティを [顧客[**パートナー関係**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship)] に設定して、新しい[customer](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer)オブジェクトを作成します。 次に、顧客識別子を使用して[**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出して顧客を指定し、 **Patch**メソッドを呼び出して新しい customer オブジェクトを渡します。

関係を再確立するには、[再販業者の関係を要求](https://docs.microsoft.com/partner-center/develop/request-reseller-relationship)するプロセスを繰り返します。 


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

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: partnersdk. FeatureSample**クラス**: DeletePartnerCustomerRelationship.cs


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST 要求   


**要求の構文**

| メソッド     | 要求 URI                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **KB830347**  | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/HTTP/1.1 |

 

**URI パラメーター**

次の表に、リセラー関係を削除するために必要なクエリパラメーターを示します。

| Name                   | 種類     | 必須 | 説明                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **顧客-テナント id** | **guid** | Y        | この値は、顧客を識別する GUID 形式の**顧客テナント id**です。 |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

要求本文には、**顧客**リソースが必要です。 **Relationshiptopartner**プロパティが [なし] に設定されていることを確認します。

**要求の例**

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

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>REST 応答


成功した場合、このメソッドは、指定された顧客の再販業者の関係を削除します。

**応答成功およびエラーコード**

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

**応答の例**

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