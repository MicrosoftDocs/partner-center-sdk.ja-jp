---
title: Console test app
description: This console test app provides sample code for all scenarios supported by the Partner Center APIs. You can also use it for testing.
ms.assetid: 56F5B4C6-CE87-4D13-9D8C-09F38E946292
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 51de7cc8b6a721c3c0d04f57d20e4d9afef50283
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488922"
---
# <a name="console-test-app"></a>Console test app

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

The console test app is provided in C# and Java, it provides sample codes for all of the scenarios supported by the Partner Center APIs. You can also use it for testing.

## <a name="get-the-code"></a>コードを入手する

Download the sample code for the console test app.

## <a name="net"></a>.NET の場合

[Download the sample code](http://go.microsoft.com/fwlink/p/?LinkId=746682) and modify it as necessary.

> [!IMPORTANT]
> Before you build the application, update the values in the *App.config* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md). Specifically, you should use your integration sandbox account settings during early development or for testing in production.

Under **ScenarioSettings** in the *App.config* file, you can set parameters that will be automatically passed into the scenarios that you run.

To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.cs* file.

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

[Download the sample code](http://go.microsoft.com/fwlink/p/?LinkId=2026887) and modify it as necessary.

> [!IMPORTANT]
> Before you build the application, update the values in the *SamplesConfigurations.json* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md). Specifically, you should use your integration sandbox account settings during early development or for testing in production.

Under **ScenarioSettings** in the *SamplesConfiguration.json* file, you can set parameters that will be automatically passed into the scenarios that you run.

To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.java* file.

## <a name="what-to-change"></a>What to change

Use the following lists to determine what to change or not change in the sample code.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

For **PartnerServiceSettings**, don't change:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

All of these settings are necessary for the sample API calls to properly function.

### <a name="userauthentication"></a>UserAuthentication

For **UserAuthentication**, you're required to change:

- **ApplicationId** (your Azure Active Directory application ID used for login)
- **UserName** (your active directory username)
- **Password** (your active directory password).

Don't change:

- **ResourceUrl**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

For **AppAuthentication**, you're required to change:

- **ApplicationId** (your active directory application ID used for application login)
- **ApplicationSecret** (your active directory application secret used for application login)
- **Domain** (your active directory domain on which the application is hosted)

### <a name="scenariosettings"></a>ScenarioSettings

For **ScenarioSettings**, don't change:

- **CustomerDomainSuffix** (the domain suffix used when creating a new customer)

Optional settings. If left blank, this information will need to be inputted when running a scenario where necessary):

- **CustomerIdToDelete** (the ID of the customer used for deletion)
- **DefaultCustomerId** (the customer ID to use in customer-related scenarios)
- **DefaultInvoiceID** (the invoice ID to use in invoice scenarios)
- **PartnerMpnId** (the partner MPN ID to use in indirect partner scenarios)
- **DefaultServiceRequestId** (the service request ID to use in service request scenarios)
- **DefaultSupportTopicID** (the support topic ID to use in service request scenarios)
- **DefaultOfferID** (the offer ID to use in offer scenarios)
- **DefaultOrderID** (the order ID to use in order scenarios)
- **DefaultSubscriptionID** (the subscription ID to use in subscription scenarios)

Optional to change. All of these settings specify the amount of entries per page when retrieving paged content:

- **CustomerPageSize**
- **InvoicePageSize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**