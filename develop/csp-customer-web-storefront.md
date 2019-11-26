---
title: CSP customer web storefront
description: This sample website code shows a working online store for customers to buy subscriptions to Microsoft products.
ms.assetid: 0726B1CA-97A1-42E6-92AD-25787BFE0C67
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b8e8a87e0ed22d1703b65085cf6eb9e1743c9f09
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489742"
---
# <a name="csp-customer-web-storefront"></a>CSP customer web storefront

適用対象:

- パートナー センター

> [!NOTE]
> This sample app applies only to the global instance of Partner Center. It does not apply to Partner Center for Microsoft Cloud Germany or to Partner Center for Microsoft Cloud for US Government.

The [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) is a **sample website** for an online store that customers can use to buy subscriptions to Microsoft products. You can modify this **sample code** for your own use to [configure the offers](#configure-offers), [add branding](#configure-branding) and [add a payment method](#configure-payment-types).

## <a name="sample-code"></a>サンプル コード

Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) from GitHub.

## <a name="configure-authentication"></a>認証設定の構成

Before you build the application, update the following values in the Web.config file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md). You should use your integration sandbox account settings during early development or for testing in production (TiP).

- **partnerCenter.applicationId**
- **partnerCenter.applicationSecret**
- **partnerCenter.domain**
- **webPortal.clientId**
- **webPortal.clientSecret**
- **webPortal.domain**
- **webPortal.azureStorageConnectionString**

## <a name="configure-offers"></a>Configure offers

You can configure the set of offers (**MicrosoftOffer**) in the **OfferCatalogViewModel**.

## <a name="configure-branding"></a>Configure branding

This sample website tracks the following company and brand information in *BrandingConfiguration.cs* and *PortalBranding.cs*:

- 組織名
- Organization logo
- Header image
- Privacy agreement
- Contact email
- Contact phone number
- Support email
- Support phone number

### <a name="configure-payment-types"></a>Configure payment types

The app currently uses a PayPal gateway, implemented in *PayPalGateway.cs*.