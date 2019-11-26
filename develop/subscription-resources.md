---
title: Subscription resources
description: Subscription resources can provide further information about subscriptions throughout the life cycle, such as support, refunds, Azure entitlements.
ms.assetid: E99B5EC3-2247-4CAD-B651-3000E36AF6B6
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: dc771fcbc8cb03e95684dd32ff0f1f29076bba49
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486702"
---
# <a name="subscription-resources"></a>Subscription resources

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

A subscription lets a customer use a service for a certain period of time. Not all fields will apply to all subscriptions. Many fields only apply at certain points in the life cycle, such as if a subscription is suspended or cancelled.

## <a name="subscription"></a>サブスクリプション

>[!NOTE]
>The **Subscription** resource has a rate limit of 500 requests per minute per tenant identifier.

The **Subscription** resource represents the life cycle of a subscription and includes properties that define the states throughout the subscription life cycle.

| プロパティ             | タスクバーの検索ボックスに                                                          | 説明                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | string                                                        | The subscription identifier.                                                                                                                                                  |
| offerId              | string                                                        | The offer identifier.                                                                                                                                                         |
| entitlementId        | string                                                        | The entitlement identifier (an Azure subscription ID).                                                                                                                        |
| offerName            | string                                                        | The offer name.                                                                                                                                                               |
| friendlyName         | string                                                        | The friendly name for the subscription defined by the partner to help disambiguate.                                                                                           |
| quantity             | number                                                        | The quantity. For example, in case of license-based billing, this property is set to the license count.                                                            |
| unitType             | string                                                        | The units defining quantity for the subscription.                                                                                                                             |
| parentSubscriptionId | string                                                        | Gets or sets the parent subscription identifier.                                                                                                                              |
| creationDate         | string                                                        | Gets or sets the creation date, in date-time format.                                                                                                                          |
| effectiveStartDate   | string in UTC date time format                                | Gets or sets the effective start date for this subscription, in date-time format. It is used to back date a migrated subscription or to align it with another.                |
| commitmentEndDate    | string in UTC date time format                                | The commitment end date for this subscription, in date-time format. For subscriptions which are not auto-renewable, this represents a date far, far away in the future.       |
| status               | string                                                        | The subscription status: "none", "active", "pending", "suspended", or "deleted".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Gets a value indicating whether the subscription is renewed automatically.                                                                                                    |
| billingType          | string                                                        | Specifies how the subscription is billed: "none", "usage", or "license".                                                                                                      |
| billingCycle         | string                                                        | Indicates the frequency with which the partner is billed for this order. Supported values are the member names found in [**BillingCycleType**](product-resources.md#billingcycletype). |
| hasPurchasableAddons | boolean                                                       | Gets or sets a value indicating whether the subscription has purchasable add-ons.                                                                                             |
| isTrial              | boolean                                                       | A value indicating whether this is a trial subscription.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | A value indicating whether this is a Microsoft product.                                                                                                                       |
| publisherName        | string                                                        | The publisher name.                                                                                                                                                           |
| actions              | 文字列の配列                                              | Gets or sets the actions that are allowed. Possible values: "edit", "cancel"                                                                                                  |
| partnerId            | string                                                        | The MPN ID of the reseller of record, used in the indirect partner model.                                                                                                     |
| suspensionReasons    | 文字列の配列                                              | Read-only. If the subscription was suspended, indicates why.                                                                                                                  |
| contractType         | string                                                        | Read-only. The type of contract: "subscription", "productKey", or "redemptionCode".                                                                                           |
| refundOptions        | array of [RefundOption](#refundoption) resources   | Read-Only. The set of refund options available for this subscription.                                                                                              |
| links                | [SubscriptionLinks](#subscriptionlinks)                       | Gets or sets the subscription links.                                                                                                                                          |
| orderId              | string                                                        | The ID of the order that was placed to begin the subscription.                                                                                                                |
| termDuration         | string                                                        | An ISO 8601 representation of the term's duration. The current supported values are **P1M** (1 month), **P1Y** (1 year) and **P3Y** (3 years).                                                        |
| 属性           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the subscription.                                                                                                                    |
| renewalTermDuration  | string                                                        | An ISO 8601 representation of the term's duration. The current supported values are **P1M** (1 month) and **P1Y** (1 year).                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

The **SubscriptionLinks** resource describes the collection of links attached to a subscription resource.

| プロパティ           | タスクバーの検索ボックスに                               | 説明                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Link](utility-resources.md#link) | Gets or sets the offer.               |
| parentSubscription | [Link](utility-resources.md#link) | Gets or sets the parent subscription. |
| product            | [Link](utility-resources.md#link) | Gets the product associated with the subscription. |
| sku                | [Link](utility-resources.md#link) | Gets the product sku associated with the subscription. |
| 可用性       | [Link](utility-resources.md#link) | Gets the product sku availability associated with the subscription. |
| activationLinks    | [Link](utility-resources.md#link) | Gets the list of activation links associated with the subscription. |
| self               | [Link](utility-resources.md#link) | The self URI.                         |
| 次へ               | [Link](utility-resources.md#link) | The next page of items.               |
| previous           | [Link](utility-resources.md#link) | The previous page of items.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

The **SubscriptionProvisioningStatus** resource provides information about the provisioning status of a subscription.

| プロパティ   | タスクバーの検索ボックスに                                                           | 説明                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | string                                                         | A GUID formatted string that identifies the product SKU.             |
| status     | string                                                         | Indicates the provisioning status: "success", "pending" or "failed". |
| quantity   | number                                                         | Provides the subscription quantity after provisioning.               |
| endDate    | string in UTC date time format                                 | The end date of the subscription.                                    |
| 属性 | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

The **SubscriptionRegistrationStatus** resource describes the collection of links attached to a subscription resource.

| プロパティ           | タスクバーの検索ボックスに                               | 説明                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | string                             | The subscription identifier.                                                          |
| status             | string                             | Indicates the registration status: "registered", "registering" or "notregistered".    |

## <a name="supportcontact"></a>SupportContact

The **SupportContact** resource represents a support contact for a customer's subscription.

| プロパティ        | タスクバーの検索ボックスに                                                           | 説明                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | string                                                         | A GUID formatted string that indicates the support contact's tenant identifier. |
| supportMpnId    | string                                                         | The contact's Microsoft Partner Network (MPN) identifier.                       |
| 名前            | string                                                         | The name of the support contact.                                                |
| links           | [ResourceLinks](utility-resources.md#resourcelinks)            | The support contact related links.                                              |
| 属性      | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes. Contains "objectType": " SupportContact".              |

## <a name="registersubscription"></a>RegisterSubscription

The **RegisterSubscription** resource returns a link that can be used to query the registration status of a subscription. The registration status is returned in the response body of a successfully accepted request to register an Azure subscription.

| プロパティ                | タスクバーの検索ボックスに                               | 説明                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | オブジェクト                             | Returns HTTP Status Code 202 "Accepted", with a Location header containing a link to query the registration status. たとえば、`"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` と記述します。 |

## <a name="refundoption"></a>RefundOption

The **RefundOption** resource represents a possible refund option for the subscription.

| プロパティ          | タスクバーの検索ボックスに | 説明                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| type | string | The type of refund. The supported values are "Partial" and "Full" |
| expiresAfter      | string in UTC date time format | The timestamp when this option expires. If null, this means it has no expiration. |

## <a name="azureentitlement"></a>AzureEntitlement

The **AzureEntitlement** resource represents the Azure entitlements for the subscription.

| プロパティ          | タスクバーの検索ボックスに | 説明                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | string | The entitlement identifier |
| friendlyName      | string | The friendly name of the entitlement. |
| status | string | The status of entitlement. |
| subscriptionId | string | The subscription identifier the entitlement belongs to. |
