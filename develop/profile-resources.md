---
title: Profile resources
description: Describes the behavior of a Cloud Solution Provider's profiles.
ms.assetid: 42F2959B-D70D-41A7-9A50-E22A2356A339
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3449aeb3695a9f286f37668d3f0862dc7b5cfa9f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486762"
---
# <a name="profile-resources"></a>Profile resources


**Applies To**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Describes the behavior of a Cloud Solution Provider's profiles.

## <a name="span-idbillingprofilespan-idbillingprofilespan-idbillingprofilebillingprofile"></a><span id="BillingProfile"/><span id="billingprofile"/><span id="BILLINGPROFILE"/>BillingProfile


Describes a partner's billing profile.

| プロパティ            | タスクバーの検索ボックスに                                                           | 説明                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| companyName         | string                                                         | The billing company name.                                   |
| address             | [Address](utility-resources.md#address)                       | The billing address address of the company or organization. |
| primaryContact      | [Contact](utility-resources.md#contact)                       | The primary contact for the company or organization.        |
| purchaseOrderNumber | string                                                         | The company or organization's purchase order number.        |
| taxId               | string                                                         | The company or organization's tax Id.                       |
| billingCurrency     | string                                                         | The currency used by the company or organization.           |
| profileType         | string                                                         | The partner profile type.                                   |
| links               | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.            |
| 属性          | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.       |

 

## <a name="span-idlegalbusinessprofilespan-idlegalbusinessprofilespan-idlegalbusinessprofilelegalbusinessprofile"></a><span id="LegalBusinessProfile"/><span id="legalbusinessprofile"/><span id="LEGALBUSINESSPROFILE"/>LegalBusinessProfile


Describes a partner's legal business profile.

| プロパティ               | タスクバーの検索ボックスに                                                           | 説明                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName            | string                                                         | The legal company name.                                                                                                                                              |
| address                | [Address](utility-resources.md#address)                       | The address of the company or organization.                                                                                                                          |
| primaryContact         | [Contact](utility-resources.md#contact)                       | The primary contact for the company or organization.                                                                                                                 |
| companyApproverAddress | [Address](utility-resources.md#address)                       | The company approver address.                                                                                                                                        |
| companyApproverEmail   | string                                                         | The company approver email.                                                                                                                                          |
| vettingStatus          | string                                                         | The vetting status. This value is the string representation of the one of the member names found in [**VettingStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus).           |
| vettingSubStatus       | string                                                         | The vetting sub-status. This value is the string representation of the one of the member names found in [**VettingSubStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus). |
| profileType            | string                                                         | The partner profile type.                                                                                                                                            |
| links                  | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.                                                                                                                     |
| 属性             | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                                                                                                                |

 

## <a name="span-idmpnprofilespan-idmpnprofilespan-idmpnprofilempnprofile"></a><span id="MpnProfile"/><span id="mpnprofile"/><span id="MPNPROFILE"/>MpnProfile


Describes a partner's Microsoft Partner Network profile.

| プロパティ    | タスクバーの検索ボックスに                                                           | 説明                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | string                                                         | The company or organization name.                     |
| mpnId       | string                                                         | The Microsoft Partner Network Id.                     |
| profileType | string                                                         | The partner profile type.                             |
| links       | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.      |
| 属性  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile. |

 

## <a name="span-idorganizationprofilespan-idorganizationprofilespan-idorganizationprofileorganizationprofile"></a><span id="OrganizationProfile"/><span id="organizationprofile"/><span id="ORGANIZATIONPROFILE"/>OrganizationProfile


Describes a partner's organization profile.

| プロパティ       | タスクバーの検索ボックスに                                                           | 説明                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | string                                                         | The organization's Id.                                                 |
| companyName    | string                                                         | The name of the company or organization.                               |
| defaultAddress | [Address](utility-resources.md#address)                       | The default address of the company or organization.                    |
| tenantId       | string                                                         | The tenant identifier.                                                 |
| domain         | string                                                         | The company or organization's domain.                                  |
| メール          | string                                                         | Gets or sets the parent subscription.                                  |
| 言語       | string                                                         | The preferred language for communication.                              |
| culture        | string                                                         | The preferred culture for communication and currency, such as "en-us". |
| profileType    | string                                                         | The partner profile type.                                              |
| links          | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.                       |
| 属性     | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                  |

 

## <a name="span-idsupportprofilespan-idsupportprofilespan-idsupportprofilesupportprofile"></a><span id="SupportProfile"/><span id="supportprofile"/><span id="SUPPORTPROFILE"/>SupportProfile


Describes a partner's support profile.

| プロパティ    | タスクバーの検索ボックスに                                                           | 説明                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| メール       | string                                                         | The email address associated with the profile.        |
| 電話   | string                                                         | The phone number associated with the profile.         |
| website     | string                                                         | The support website.                                  |
| profileType | string                                                         | The partner profile type.                             |
| links       | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.      |
| 属性  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile. |

 

 

 




