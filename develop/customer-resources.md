---
title: Customer resources
description: Customer resources that represent a customer or reseller.
ms.assetid: C7EC2657-62F2-43B3-B171-2F74498D45E0
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 09dd70431b34ad5c63820931113a71908b24acd0
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489702"
---
# <a name="customer-resources"></a>Customer resources

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

## <a name="customer"></a>お客様

The **Customer** resource represents a customer or reseller. Most broadly, a customer resouce can be any person, employee, or organization that wishes to do business with Microsoft and Microsoft's resellers. Customers also have a company profile and a billing profile.

>[!NOTE]
>The **Customer** resource has a rate limit of 500 requests per minute per tenant identifier.

| プロパティ              | タスクバーの検索ボックスに                                                             | 説明                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | string                                                           | The customer ID.                                                                                                                             |
| commerceId            | string                                                           | The commerce ID.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Additional information about the company or organization.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Additional information used for billing.                                                                                                     |
| relationshipToPartner | string                                                           | Defines the licensing program that the partner uses for this customer: "none", "reseller", "advisor", "syndication" or "microsoft\_support". |
| allowDelegatedAccess  | boolean                                                          | Whether the partner has been granted delegated admin privileges by this customer.                                                            |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | The user credentials.                                                                                                                        |
| customDomains         | 文字列の配列                                                 | List of custom domains of a customer.                                                                                                        |
| associatedPartnerId   | string                                                           | The indirect reseller associated to this customer account. This value can be set only by indirect CSP partners.                              |
| links                 | [ResourceLinks](utility-resources.md#resourcelinks)             | The resource links contained within the profile.                                                                                             |
| 属性            | [ResourceAttributes](utility-resources.md#resourceattributes)   | The metadata attributes corresponding to the profile.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

The **CustomerCompanyProfile** resource is additional information about the company or organization.

| プロパティ    | タスクバーの検索ボックスに                                                           | 説明                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | string                                                         | The customer's tenant identifier for Azure AD. This is also called a MicrosoftID. |
| domain      | string                                                         | The customer's name, such as contoso.onmicrosoft.com.                             |
| companyName | string                                                         | The name of the company or organization.                                          |
| links       | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links contained within the profile.                                  |
| 属性  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                             |

## <a name="customerbillingprofile"></a>CustomerBillingProfile

The **CustomerBillingProfile** resource is additional information used for billing the customer.

| プロパティ       | タスクバーの検索ボックスに                                                           | 説明                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | string                                                         | The profile identifier.                                                                                                                                |
| firstName      | string                                                         | The first name of the billing contact at the customer's company. This is the person that invoices and other billing communication will be directed to. |
| lastName       | string                                                         | The last name of the billing contact.                                                                                                                  |
| メール          | string                                                         | The billing contact's email address                                                                                                                    |
| culture        | string                                                         | Their preferred culture for communication and currency, such as "en-us".                                                                               |
| 言語       | string                                                         | Their preferred language for communication.                                                                                                            |
| companyName    | string                                                         | The name of the company or organization.                                                                                                               |
| defaultAddress | [Address](utility-resources.md#address)                       | The address that bills are sent to, where the billing contact works.                                                                                   |
| links          | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links contained within the profile.                                                                                                       |
| 属性     | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

The **CustomerRelationshipRequest** resource contains the URL used by the customer to establish a reseller relationship with a partner.

| プロパティ   | タスクバーの検索ボックスに                                                           | 説明                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | string                                                         | The URL used by the customer to establish a relationship with a partner. |
| 属性 | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the relationship request.       |