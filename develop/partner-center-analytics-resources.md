---
title: Partner Center Analytics
description: Partner Center Analytics public API documentation.
ms.assetid: B605C1CD-FC40-4393-8588-55C8F0CAA51A
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ce7245e3a556b038b8f71ba5fef9ea96c13f4869
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486882"
---
# <a name="partner-center-analytics---resources"></a>Partner Center Analytics - Resources

**Applies To**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター


The Analytics API allows you to programmatically access data that is being presented in the User Experience. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). These scenarios support authentication with User credentials only.


## <a name="span-idazure_usage_analyticsspan-idazure_usage_analyticsspan-idazure_usage_analyticscsp-program-azure-usage-analytics"></a><span id="Azure_Usage_Analytics"/><span id="azure_usage_analytics"/><span id="AZURE_USAGE_ANALYTICS"/>CSP program: Azure usage analytics

The following scenario shows you how to use the Analytics API to retrieve all your Partner Center Azure usage analytics information.  

- [Get all Azure usage analytics information](get-all-azure-usage-analytics.md)  

This scenario returns your analytics information in a collection of [Azure usage](#azure_usage) resources. 

## <a name="span-idazure_usagespan-idazure_usagespan-idazure_usageazure-usage-resource"></a><span id="Azure_Usage"/><span id="azure_usage"/><span id="AZURE_USAGE"/>Azure usage resource

Represents all of the analytical data for Azure usage.

| プロパティ | タスクバーの検索ボックスに | 説明 |
|----------|------|-------------|
| CustomerTenantId | string | The customer tenant identifier. |
| customerName | string | The customer name. |
| subscriptionId | string | The subscription identifier. |
| subscriptionName | string | The subscription name. |
| usageDate | string | The usage date. |
| resourceLocation | string | The location of the data center, Western Europe, for example. |
| meterCategory | string | The meter category, data management, for example. |
| meterSubcategory | string | The meter subcategory, for example, geo redundant. |
| meterUnit | string | The meter unit, such as gigabytes or hours. | 
| reservationOrderId | string | The reservation order for an Azure VM Reserved Instance. |
| reservationId | string | Reserved instances under a specific RI order. |
| serviceType | string | Indicates the virtual machine type. For example, Standard_E4s_v3. |
| quantity | long | Indicates the numbers used in the meter unit. |


## <a name="span-idindirect_resellers_analyticsspan-idindirect_resellers_analyticsspan-idindirect_resellers_analyticscsp-program-indirect-resellers-analytics"></a><span id="Indirect_Resellers_Analytics"/><span id="indirect_resellers_analytics"/><span id="INDIRECT_RESELLERS_ANALYTICS"/>CSP program: indirect resellers analytics

The following scenario shows you how to use the Analytics API to retrieve all your Partner Center indirect resellers analytics information.  

- [Get all indirect resellers analytics information](get-all-indirect-resellers-analytics.md)  

This scenario returns your analytics information in a collection of [indirect resellers](#indirect_resellers) resources. 


## <a name="span-idindirect_resellersspan-idindirect_resellersspan-ididirect_resellersindirect-resellers-resource"></a><span id="Indirect_Resellers"/><span id="indirect_resellers"/><span id="IDIRECT_RESELLERS"/>Indirect resellers resource

Represents all of the analytical data for indirect resellers.

| プロパティ | タスクバーの検索ボックスに | 説明 |
|----------|------|-------------|
| partnerTenantId | string | The Tenant ID of the partner for which you want to retrieve indirect resellers data. |
| id | string | Indirect reseller ID. |
| 名前 | string | The Name of the partner for which you want to retrieve indirect resellers data. |
| market | string | The Market of the partner for which you want to retrieve indirect resellers data. |
| firstSubscriptionCreationDate | string in UTC date time format | The creation date of the first subscription based on which you want to retrieve indirect resellers data. |
| latestSubscriptionCreationDate | string in UTC date time format | The creation date of the latest subscription. |
| firstSubscriptionEndDate | string in UTC date time format | First time any subscription was ended. |
| latestSubscriptionEndDate | string in UTC date time format | Latest date when any subscription was ended. |
| firstSubscriptionSuspendedDate | string in UTC date time format | First time any subscription was suspended. |
| latestSubscriptionSuspendedDate | string in UTC date time format | Latest date when any subscription was suspended. |
| firstSubscriptionDeprovisionedDate | string in UTC date time format | First time any subscription was deprovisioned. |
| latestSubscriptionDeprovisionedDate | string in UTC date time format | Latest date when any subscription was deprovisioned. |
| subscriptionCount | double | Subscription count for all value added resellers |
| licenseCount | double | License count for all value added resellers |
| indirectResellerCount | double | Indirect resellers count |


## <a name="span-idsubscription_analyticsspan-idsubscription_analyticsspan-idsubscription_analyticscsp-program-subscription-analytics"></a><span id="Subscription_Analytics"/><span id="subscription_analytics"/><span id="SUBSCRIPTION_ANALYTICS"/>CSP program: subscription analytics

The following scenarios show you how to use the Analytics API to retrieve all your Partner Center subscription analytics information, filter it with a search query, or group it by dates or terms.  

- [Get all subscription analytics information](get-all-subscription-analytics.md)  
- [Get subscription analytics information filtered by a search query](get-subscription-analytics-by-search-query.md)  
- [Get subscription analytics information grouped by dates or terms](get-subscription-analytics-grouped-by-dates-or-terms.md)  

All of these scenarios return your analytics information in a collection of [Subscription](#subscription) resources. 


## <a name="span-idsubscriptionspan-idsubscriptionspan-idsubscriptionsubscription-resource"></a><span id="Subscription"/><span id="subscription"/><span id="SUBSCRIPTION"/>Subscription resource


Represents all of the analytical data for a subscription.


|         プロパティ          |              タスクバーの検索ボックスに              |                                                                      説明                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     customerTenantId      |             string             |                                              A GUID-formatted string that identifies the customer tenant.                                              |
|       customerName        |             string             |                                                               The name of the customer.                                                                |
|      customerMarket       |             string             |                                                 The country/region that the customer does business in.                                                 |
|            id             |             string             |                                                              The subscription identifier.                                                              |
|          status           |             string             |                                          The subscription status: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".                                           |
|        productName        |             string             |                                                                製品の名前。                                                                |
|     subscriptionType      |             string             |       The subscription type. **Note**: This field is case sensitive. Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".       |
|     autoRenewEnabled      |            boolean             |                                         A value indicating whether the subscription is renewed automatically.                                          |
|         partnerId         |             string             | The MPN ID. For a direct reseller, this will be the MPN ID of the partner. For an indirect reseller, this will be the MPN ID of the indirect reseller. |
|       friendlyName        |             string             |                                                             The name of the subscription.                                                              |
|        partnerName        |             string             |                                              Name of the partner for whom the subscription was purchased                                               |
|       providerName        |             string             |            When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.             |
|    effectiveStartDate     | string in UTC date time format |                                                           The date the subscription starts.                                                            |
|     commitmentEndDate     | string in UTC date time format |                                                            The date the subscription ends.                                                             |
|    currentStateEndDate    | string in UTC date time format |                                           The date that the current status of the subscription will change.                                            |
| trialToPaidConversionDate | string in UTC date time format |                                 The date that the subscription converts from trial to paid. 既定値は null です。                                 |
|      trialStartDate       | string in UTC date time format |                                The date that the trial period for the subscription started. 既定値は null です。                                 |
|       trialEndDate        | string in UTC date time format |                                  The date that the trial period for the subscription ends. 既定値は null です。                                  |
|       lastUsageDate       | string in UTC date time format |                                        The date that the subscription was last used. 既定値は null です。                                        |
|     deprovisionedDate     | string in UTC date time format |                                      The date that the subscription was deprovisioned. 既定値は null です。                                      |
|      lastRenewalDate      | string in UTC date time format |                                       The date that the subscription was last renewed The default value is null.                                       |
|       licenseCount        |             number             |                                                             The total number of licenses.                                                              |
|     subscriptionCount     |             number             |                        The number of subscriptions. Note: This value will only appear in the response of an aggregation query.                         |

## <a name="span-idsearch_analyticsspan-idsearch_analyticsspan-idsearch_analyticssearch-analytics"></a><span id="Search_Analytics"/><span id="search_analytics"/><span id="SEARCH_ANALYTICS"/>Search analytics

> [!NOTE]  
> CSP program membership is not required to get search analytics.

The following scenario shows you how to use the Analytics API to retrieve all your Partner Center search analytics information.  

- [Get all search analytics information](get-all-search-analytics.md)  

This scenario returns your analytics information in a collection of [Search](#search_resource) resources. 


## <a name="span-idsearch_resourcespan-idsearch_resourcespan-idsearch_resourcesearch-resource"></a><span id="Search_Resource"/><span id="search_resource"/><span id="SEARCH_RESOURCE"/>Search resource

Represents all of the analytical data for a search.

| プロパティ | タスクバーの検索ボックスに | 説明 |  
|----------|------|-------------|  
| companyName | string | The billing company name. |
| contactButtonClicked | Boolean | Indicates if the contact button was clicked. |
| keywordCountry | string | The country specified in the search. |
| detailsViewed | Boolean | Indicates if search details were viewed. |
| keywordIndustryFocus | string | The industry to search within, for example, healthcare. |
| mpnId | string | The Microsoft Partner Network (MPN) ID. For a direct reseller, this will be the MPN ID of the partner. For an indirect reseller, this will be the MPN ID of the indirect reseller. |
| partnerMarket | string | Locale where the partner conducts business. |
| keywordProduct | string | The product specified in the search. |
| referralSubmitted | Boolean | Indicates if a referral was submitted. |
| searchDate | string in UTC date time format | Date when the search query occurred. |
| keywordSearchText | string | The text specified in the search. |
| searchResultPageViews | long | Number of times the partner came up in the search result. Part of a response only on aggregation.
| contactClicks | long | Number of times the contact button was clicked. Part of a response only on aggregation.
| referralCount | long | Number of referrals generated from the search. Part of a response only on aggregation.
| profileViews | long | Number of times the partner profile was viewed. Part of a response only on aggregation.


## <a name="span-idreferral_analyticsspan-idreferral_analyticsspan-idreferral_analyticsreferrals-analytics"></a><span id="Referral_Analytics"/><span id="referral_analytics"/><span id="REFERRAL_ANALYTICS"/>Referrals analytics

> [!NOTE]  
> CSP program membership is not required to get referrals analytics.

The following scenario shows you how to use the Analytics API to retrieve all your Partner Center referrals analytics information.  

- [Get all referrals analytics information](get-all-referrals-analytics.md)  

This scenario returns your analytics information in a collection of [Referrals](#referrals) resources. 

> [!NOTE]  
> Referrals analytics are not available to the Partner Center operated by 21Vianet. 


## <a name="span-idreferralsspan-idreferralsspan-idreferralsreferrals-resource"></a><span id="Referrals"/><span id="referrals"/><span id="REFERRALS"/>Referrals resource

Represents all of the analytical data for a referral.

| プロパティ | タスクバーの検索ボックスに | 説明 |
|----------|------|-------------|
| id | string | The customer tenant identifier.  |
| status | string | Indicates if the referral led to a customer.  |
| customerMarket | string | The country/region that the customer does business in. |
| customerName | string | The name of the customer. |
| customerOrgSize | string | A range indicating the number of employees in the customer's organization. For example, "10to50employees". |
| acceptedDate | string in UTC date time format | The date that the referral was accepted. |
| acknowledgedDate | string in UTC date time format | The date that the referral was acknowledged. |
| archivedDate | string in UTC date time format | The date that the referral was archived. |
| declinedDate | string in UTC date time format | The date that the referral was declined. |
| expiredDate | string in UTC date time format | The date that the referral expired. |
| lostDate | string in UTC date time format | The date that the referral was lost. |
| missedDate | string in UTC date time format | The date that the referral was missed. |
| createdDate | string in UTC date time format | The date that the referral was created. |
| skippedDate | string in UTC date time format | The date that the referral was skipped. |
| wonDate | string in UTC date time format | The date that the referral was won. |
| partnerMarket | string |  The country/region that the partner does business in. |  
