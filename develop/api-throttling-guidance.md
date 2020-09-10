---
title: API 調整のガイダンス
description: 調整が発生する場合
ms.date: 09/09/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: a9fa70f8343ed51b288c1385540a247844e4659a
ms.sourcegitcommit: b3a8b6db5fee1cb8756b94105f358ed4bc94d3a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89666627"
---
# <a name="api-throttling-guidance"></a>API 調整のガイダンス 

**適用対象**

- パートナー センター

Microsoft は、パートナーセンター API を呼び出しているパートナーの期間内で、より一貫したパフォーマンスを実現するために API 調整を実装しています。 スロットルでは、リソースが過剰に活用されるのを防ぐために、サービスに対する要求の数を時間単位で制限します。 パートナーセンターは大量の要求を処理するように設計されていますが、少数のパートナーから膨大な数の要求が発生した場合、調整によって、すべてのパートナーにとって最適なパフォーマンスと信頼性を維持できます。  

スロットルの制限は、シナリオによって異なります。 たとえば大量の書き込みを実行している場合、読み取りだけを実行している場合と比べて、スロットルの余地は大きくなります。

## <a name="what-happens-when-throttling-occurs"></a>スロットルが発生した場合の動作 

制限のしきい値を超えた場合、パートナーセンターは、そのクライアントからのその他の要求を一定期間制限します。 スロットルの動作は、要求の種類と数によって異なります。   

### <a name="common-throttling-scenarios"></a>スロットルの一般的なシナリオ 

スロットルが発生する最も一般的なクライアント側の原因には、次のようなものがあります。 

- **パートナーのテナント id ごとの api に対する多数の要求**: パートナーセンターの api によっては、パートナーのテナント id によって調整が行われますが、同じパートナーのテナント id でこれらの api の呼び出しが多すぎると、制限のしきい値を超えることになります。  

- パートナーのテナント id ごとの**api に対する多数の要求 (顧客**のテナント id ごと): 他の api の場合、調整はパートナーのテナント Id/顧客のテナント id の組み合わせによって決定されます。このような場合、同じ顧客のテナント ID に対する呼び出しが多すぎると、調整が行われますが、他の顧客に対する問い合わせは成功する可能性があります。

## <a name="best-practices-to-avoid-throttling"></a>調整を回避するためのベストプラクティス 
 
リソースを継続的にポーリングして更新プログラムを確認したり、リソースコレクションを定期的にスキャンして新規または削除されたリソースを確認するなどのプログラミングプラクティスでは、調整が行われ、全体的なパフォーマンスが低下する可能性があります。 同時実行 API 呼び出しによって、ユニット時間あたりの要求数が多くなり、要求が調整されることもあります。 代わりに、変更の追跡と変更通知を活用する必要があります。 さらに、アクティビティログを利用して変更を検出することもできます。詳細については、「 [パートナーセンターのアクティビティログ](get-a-record-of-partner-center-activity-by-user.md) 」を参照してください。  効率性を高め、スロットルを回避するために、アクティビティログ API の使用を検討することを強くお勧めします。 後述の「アクティビティログの使用例」も参照してください。

## <a name="best-practices-to-handle-throttling"></a>スロットル処理のベスト プラクティス

調整を処理するためのベストプラクティスを次に示します。 

- 並列処理の次数を下げます。 
- 呼び出しの頻度を減らす。 
- すべての要求が使用制限に対して発生するため、すぐに再試行することは避けてください。 

エラー処理を実装する場合は、HTTP エラーコード429を使用して調整を検出します。 失敗した応答には、再試行後の応答ヘッダーが含まれます。 再試行の遅延を使用して要求をオフにすることは、スロットルから回復する最も簡単な方法です。 

再試行後の待ち時間を使用するには、次の手順を実行します。 

1. 再試行ヘッダーで指定した秒数だけ待機します。 

2. 要求をやり直してください。  

3. 429エラーコードによって要求が再度失敗した場合は、まだ調整されています。 指数バックオフを使用して再試行し、推奨される再試行後の遅延を使用して、要求が成功するまで再試行します。

## <a name="apis-currently-impacted-by-throttling"></a>API は現在調整の影響を受けています

長時間実行では、エンドポイント "api.partnercenter.microsoft.com/" を呼び出す単一のパートナーセンター API がすべて調整されます。 現時点では、スロットルの制限は、以下に示すいくつかの API にのみ適用されます。 パートナーセンターは、各 API のテレメトリを収集し、調整制限を動的に調整します。 次の表に、スロットルが現在適用されている API の一覧を示します。  


|**操作**| **パートナー センターのドキュメント**|       
|------------------------|----------------------------|
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions|すべてのユーザー-s-s-サブスクリプション|    
|https://api.partnercenter.microsoft.com/v1/productUpgrades/eligibility|利用資格-製品-アップグレード|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}|id でサブスクリプションを取得する|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders|すべての顧客の注文を取得する|     
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders/{order_id}|id で注文を取得する|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus|サブスクリプションのプロビジョニング状態の取得|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}|注文の管理とサブスクリプションの管理|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons|サブスクリプションのアドオンの一覧を取得する|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements|サブスクリプションに対する azure の権利の一覧を取得する|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders|注文を作成する|     
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus|サブスクリプション登録状態の取得|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades|サブスクリプションを移行する|          
|https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/transfers|すべてのお客様の譲渡|   
|https://api.partnercenter.microsoft.com/v1/productUpgrades/{upgrade-id}/status|製品のアップグレード状態の取得| 
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders/{order_id}|id で注文を取得する|           
|https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/orders/{order-id}|サブスクリプションへのアドオンを購入する|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/carts/{cart-id}|カートを作成する|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/carts/{cart-id}/checkout|カートをチェックアウトする|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/carts/{cart-id}|カートを更新する|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations|サブスクリプションを登録する|  
|https://api.partnercenter.microsoft.com/v1/productupgrades|製品のアップグレードエンティティの作成|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions|
試用版変換プランの一覧を取得する|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions|
試用版サブスクリプションを有料に変換する|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}|id で顧客を取得する|

### <a name="error-code-response"></a>エラーコードの応答:

HTTP/1.1 429 要求が多すぎます 

Content-length:84 

Content-Type, application/json 

再試行-後:57 

日付: 火曜日、21月 2020 04:10:58 GMT 

{"statusCode": 429, "message": "レート制限を超えました。 57秒後にもう一度やり直してください。 " } 


## <a name="example-of-activity-log"></a>アクティビティログの例

毎日の変更を分析するためのベストプラクティスとして、特定の日の監査レコードを照会することをお勧めします。 

応答では、特定の操作の種類を変更した結果が得られます。注意する操作に基づいてフィルター処理できます。 たとえば、新しく作成された顧客に関心がある場合は、operationType = "add_customer" を参照してください。  

Operationtype/リソースの一覧については、以下の API ドキュメントを参照してください。  

- [リソースの監査](https://docs.microsoft.com/partner-center/develop/auditing-resources)  

- [パートナーセンターのアクティビティのレコードをユーザー別に取得する](https://docs.microsoft.com/partner-center/develop/get-a-record-of-partner-center-activity-by-user)  



### <a name="response-example"></a>応答の例

**要求**:  

Http Get 呼び出し: https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50 

承認: ベアラー <token> 

Accept: application/json 

MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893 

MS CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14 

X-Locale: en-us 

ホスト: api.partnercenter.microsoft.com 

接続: キープアライブ 

**応答**:    
```http
{ 

    "totalCount": 17, 

    "items": [ 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_e905b566-4779-4e57-944c-7b1b5312705b_updatecustomeruserlicenses_637346859797753934", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "e905b566-4779-4e57-944c-7b1b5312705b", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "FulfillmentService", 

            "resourceType": "license", 

            "operationType": "update_customer_user_licenses", 

            "operationDate": "2020-09-02T23:26:19.7753934Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "CustomerUserId", 

                    "value": "933808c7-b165-496c-a24e-1a4b7846fab4" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_ia80zlkxp6ewoqpp35pbqjlhqv9iigvz1_createorder_637346662909268372", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "order", 

            "resourceNewValue": "{\"Id\":\"Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"AlternateId\":\"64144d300bde\",\"ReferenceCustomerId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"BillingCycle\":\"monthly\",\"CurrencyCode\":\"USD\",\"CurrencySymbol\":\"$\",\"LineItems\":[{\"LineItemNumber\":0,\"ProvisioningContext\":null,\"OfferId\":\"DZH318Z0C964:0001:DZH318Z0BZDG\",\"SubscriptionId\":\"f428d44a-d08b-348b-579e-ce92a6362c7b\",\"ParentSubscriptionId\":null,\"TermDuration\":\"P1M\",\"TransactionType\":\"New\",\"FriendlyName\":\"SaaS custom meter offer - Bronze\",\"Quantity\":1,\"Pricing\":null,\"PartnerIdOnRecord\":null,\"RenewsTo\":null,\"Links\":{\"Product\":{\"Uri\":\"/products/DZH318Z0C964?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Sku\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Availability\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001/availabilities/DZH318Z0BZDG?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ActivationLinks\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/lineitems/0/activationlinks\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}}}],\"CreationDate\":\"2020-09-02T17:58:01.7755853Z\",\"Status\":\"pending\",\"TransactionType\":\"UserPurchase\",\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ProvisioningStatus\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/provisioningstatus\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"PatchOperation\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"PATCH\",\"Body\":null,\"Headers\":[]}},\"Client\":{\"marketplaceCountry\":\"US\",\"deviceFamily\":\"UniversalStore-PartnerCenter\",\"name\":\"Partner Center Web\"},\"Attributes\":{\"ObjectType\":\"Order\"}}", 

            "operationType": "create_order", 

            "originalCorrelationId": "96514ebe-c1b2-4865-cb46-2c2d20a2e911", 

            "operationDate": "2020-09-02T17:58:10.9268372Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "OrderId", 

                    "value": "Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1" 

                }, 

                { 

                    "key": "AlternateId", 

                    "value": "64144d300bde" 

                }, 

                { 

                    "key": "BillingCycle", 

                    "value": "Monthly" 

                }, 

                { 

                    "key": "OfferId-0", 

                    "value": "DZH318Z0C964:0001:DZH318Z0BZDG" 

                }, 

                { 

                    "key": "SubscriptionId-0", 

                    "value": "f428d44a-d08b-348b-579e-ce92a6362c7b" 

                }, 

                { 

                    "key": "SubscriptionName-0", 

                    "value": "SaaS custom meter offer - Bronze" 

                }, 

                { 

                   "key": "Quantity-0", 

                    "value": "1" 

                }, 

                { 

                    "key": "PartnerOnRecord-0", 

                    "value": null 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                           { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_86bddccf-9a53-40c6-907c-08067a3f8da7_addcustomer_637346648528069005", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "customer", 

            "resourceNewValue": "{\"Id\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"CommerceId\":\"9dd78b4f-f98a-44b4-a2fa-2b82ac58d24c\",\"CompanyProfile\":{\"TenantId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"Domain\":\"CustomMetersStagingTest.onmicrosoft.com\",\"CompanyName\":\"CustomMetersStagingTest\",\"Address\":null,\"Email\":null,\"OrganizationRegistrationNumber\":null,\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/profiles/company\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}},\"Attributes\":{\"ObjectType\":\"CustomerCompanyProfile\"}},\"BillingProfile\":{\"Id\":\"4beafd7b-cdab-5bdc-52ed-02e16edf2e7a\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"Email\":\"CustomMetersStagingTest@CustomMetersStagingTest.com\",\"Culture\":\"en-US\",\"Language\":\"en\",\"CompanyName\":\"CustomMetersStagingTest\",\"DefaultAddress\":{\"Id\":null,\"Country\":\"US\",\"Region\":null,\"City\":\"Seattle\",\"State\":\"WA\",\"District\":null,\"AddressLine1\":\"CustomMetersStagingTest\",\"AddressLine2\":null,\"AddressLine3\":null,\"PostalCode\":\"98122\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"EmailAddress\":null,\"PhoneNumber\":null,\"MiddleName\":null},\"Attributes\":{\"Etag\":\"-2279334701316321663\",\"ObjectType\":\"CustomerBillingProfile\"}},\"RelationshipToPartner\":\"reseller\",\"AllowDelegatedAccess\":true,\"UserCredentials\":{\"userName\":\"admin\",\"password\":\"\"},\"AssociatedPartnerId\":null,\"CustomDomains\":null,\"Attributes\":{\"ObjectType\":\"Customer\"}}", 

            "operationType": "add_customer", 

            "originalCorrelationId": "7550d9ea-e64a-416f-e49b-3670c516cf69", 

            "operationDate": "2020-09-02T17:34:12.8069005Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "PrimaryDomainName", 

                    "value": "CustomMetersStagingTest.onmicrosoft.com" 

                }, 

                { 

                    "key": "Relationship", 

                    "value": "Reseller" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                            

        ... 

    ], 

    "links": { 

        "self": { 

            "uri": "/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50", 

            "method": "GET", 

            "headers": [] 

        } 

    }, 

    "attributes": { 

        "objectType": "Collection" 

    } 

} 
```
 

  
