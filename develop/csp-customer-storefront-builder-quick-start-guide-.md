---
title: CSP Customer Storefront Builder Quick Start Guide
description: Create an online marketplace to sell cloud solution provider (CSP) offers using the CSP Customer Storefront Builder.
ms.assetid: 333EE80D-E49E-4E89-87FB-3F02AC48C236
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2b36d1f64a9ab02483832674997c66e3fbffd36e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489732"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>CSP Customer Storefront Builder Quick Start Guide

適用対象:

- パートナー センター

Create an online marketplace to sell cloud solution provider (CSP) offers by using the CSP Customer Storefront Builder.

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>Introduction to the CSP Customer Storefront Builder

The CSP Customer Storefront Builder helps partners easily create an online marketplace to sell CSP offers to their customers. Most partners and small sales organizations want to focus on selling rather than developing an online marketplace. The Partner Center SDK sample app requires software development skills to create and deploy a website. With the CSP Customer Storefront Builder, you can quickly and easily create your own website. You can also download the website as sample code or deploy directly to your Azure subscription with a Ready to Transact website.

This website is fully owned, supported, and maintained by partners, and Microsoft does not collect any data or telemetry from the website. The CSP Customer Storefront Builder creates a website for the partner that is fully compliant with the [Payment Card Industry Data Security Standard](https://www.pcisecuritystandards.org/) (PCI DSS).

The CSP Customer Storefront Builder code is subject to the license available in the [Partner Center SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK).

>[!NOTE]
>You are responsible for the storefront website management, maintenance, and any issues that might result from website creation. Read and understand the terms in the [Partner Center SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK).

For additional information, also see the following topics: [CSP customer web storefront](csp-customer-web-storefront.md) and [console test app](console-test-app.md).

## <a name="considerations"></a>考慮事項

The CSP Customer Storefront Builder is intended as a quick way to create a website. Be aware of the following considerations during your planning:

- Once deployed, Microsoft and Partner Center does not maintain a copy of the partner website or any information added into the CSP Customer Storefront Builder.
- Partner Center can only deploy a CSP Customer Storefront website to a partner's Azure subscriptions.
- This website, once deployed, is fully owned and managed by the partner. Microsoft does not have access to this website, or any data related to the website. Partners are responsible for maintenance and management of the website. Microsoft will not provide any live website or other support related to the CSP Customer Storefront Builder or any website created by using the CSP Customer Storefront Builder.
- Partner Center cannot directly access or upgrade this website with new or changed SDK or API features. Any new features or enhancements must be owned, developed, and managed by partners, including adding new Partner Center SDK or API features.
- This CSP Customer Storefront Builder currently provides the ability to configure payment to a PayPal Pro/PayU Money (for India) account. If partners need to change the payment processor, they will need to change the code to support their preferred payment method.
- Any payment related information added in the CSP Customer Storefront Builder is not stored or maintained in Partner Center.
- PayPal payment configuration will work in any geographies where PayPal is available. PayPal availability and support is solely controlled by PayPal, and may be discontinued at any time by PayPal.
- PayU payment configuration will work only in India currently. PayU availability and support is solely controlled by PayU and may be discontinued at any time by PayU.
- Read and understand the terms in the [Partner Center SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK).

## <a name="using-the-csp-customer-storefront-builder"></a>Using the CSP Customer Storefront Builder

CSP partner admins on Partner Center can deploy a CSP Customer Storefront directly from Partner Center. With minimal effort, a new website can be deployed on the partner's tenant. Once deployed, partners can use the website to configure branding, offers, and payment-related information, and then share the website URL address with customers.

The process for creating a storefront website is to:

1. [Deploy the website](#deploy)
2. [Configure the storefront](#configure)
3. [Transact on the storefront](#transact)

### <a name="deploy"></a>展開

展開オプション:

- Deploy your website from Partner Center
- Integrate with Azure to deploy the configured website
- Deploy on an existing subscription or bring your own subscription

### <a name="configure"></a>構成

No development skills are required to customize a storefront.

Log in with your Partner Center admin credentials to configure:

- **Branding**: company name, logo, contacts, and more.
- **Offers**: view all CSP offers. You can select which offers your customers can view and purchase. You can also personalize offer information and add your price.
- **PayPal payment configuration**: add your PayPal payment account information. If you don't have a PayPal account, you can visit <https://www.paypal.com> and create a new account. This account will be used for PayPal to credit the payments made by customers. *Microsoft is not responsible for the relationship between partners and PayPal. Use of PayPal may require the partner or partner's customers to agree to additional terms.*
- (*For India*) **PayU Payment configuration**: add your PayU Money payment account information. If you don't have a PayU Money account, you can visit <https://www.payumoney.com/> and create a new account. This account will be used for PayU to credit the payments made by customers. *Microsoft is not responsible for the relationship between partners and PayU. Use of PayU may require the partner or partner's customers to agree to additional terms.*

### <a name="transact"></a>Transact

- After deployment, customers can immediately purchase and transact.
- Customers can buy directly from the partner portal integrated with the Partner Center SDK.

#### <a name="customer-countries"></a>Customer countries

Customers can belong to these countries:

| 国コード | Country Name   |
|--------------|----------------|
| AU           | オーストラリア      |
| AT           | オーストリア        |
| BE           | ベルギー        |
| BG           | ブルガリア       |
| CA           | カナダ         |
| HR           | クロアチア        |
| CY           | キプロス         |
| CZ           | チェコ共和国 |
| DK           | デンマーク        |
| EE           | エストニア        |
| FI           | フィンランド        |
| FR           | フランス         |
| DE           | ドイツ        |
| GR           | ギリシャ         |
| HU           | ハンガリー        |
| IS           | アイスランド        |
| IN           | インド          |
| Internet Explorer           | アイルランド        |
| IT           | イタリア          |
| JP           | 日本          |
| LV           | ラトビア         |
| LI           | リヒテンシュタイン  |
| LT           | リトアニア      |
| LU           | ルクセンブルク     |
| MT           | マルタ          |
| [MC]           | モナコ         |
| NL           | オランダ    |
| NZ           | ニュージーランド    |
| 使用不可           | ノルウェー         |
| PO           | ポーランド         |
| PT           | ポルトガル       |
| RO           | ルーマニア        |
| SK           | スロバキア       |
| SL           | スロベニア       |
| ES           | スペイン          |
| SE           | スウェーデン         |
| CH           | スイス    |
| GB           | 英国 |
| US           | 米国  |

### <a name="additional-resources"></a>その他の資料

To enhance or customize your CSP Customer Storefront:

- Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) make additional customizations.
- Use Microsoft Visual Studio 2015 (or later) to develop.
- Build for additional changes and enhancements (including authorizations, certifications, manifest changes, and other items).

## <a name="partner-experience-scenarios"></a>Partner experience scenarios

### <a name="deployment-scenario"></a>展開方法

- A partner admin can use Partner Center to deploy the website. In Account settings, choose **Web storefront** to deploy a new website.
- On this page, partners can see the availability of a new site name and change it (if available).
- This page shows all active Azure subscriptions associated to this partner tenant and that a partner can choose to use to deploy the website.
- If a partner does not have an active subscription associated to this Partner Center account, they can add this account as an admin to an existing Azure subscription, and refresh to see that subscription in this list.
- Partners choose the data center location where this website will be deployed.
- The **Deploy your store** link will deploy this new website based on the information provided and show the URL.
- Be sure to copy this URL as Partner Center does not maintain the state or history of these websites. If you close the browser page, you will lose the website name.
- During deployment, the website will be deployed with the web app credentials created in Partner Center. If you did not register a web app, this will be registered during deployment.

### <a name="configuration-scenario"></a>Configuration scenario

- The newly created website is linked to a partner tenant and has access to all admin accounts of this partner tenant.
  -Partners can log in to this new website using their Partner Center admin credentials.
- The storefront application currently supports French, Spanish, Dutch, German, Japanese and English. (English serves as the fallback language.)
  - The storefront configures the locale by using the partner's default locale from the partner's profile in the Partner Center. This locale is used to configure currencies, date formats, and localized offers in the repository.
- Partners can configure branding, offers and PayPal or PayU (for India) payment information.
- Partners can update the company name, company logo, header image, sales and support contacts and more.
- Partners can see all CSP offers available based on their territory.
  - Partners can choose which offers they want to show to all of their customers.
  - A CSP partner can select one or more offers and update the name, quantity, feature description, and price.
  - The price is the annual price. Customers subscribe annually.
- Partners can at any time configure pre-approved transactions for (a) all current and future customers OR (b) specific customers.
  - Pre-approved customers are not required to pay on the portal when they add new subscriptions, purchase additional seats to existing subscriptions, or renew a subscription.
  - Pre-approved customers will not be redirected to PayPal or PayU (for India) for payment during these transactions.
  - Pre-approved customer transactions allow a partner to perform offline billing and invoicing to their pre-approved customers.
- A CSP partner can input their PayPal account information such as PayPal Client ID and secret. A CSP partner can also select whether they want to test using a sandbox or a live account.
  - Partners can find this information on <https://developer.paypal.com/> in **my apps & credentials**. You can also get this information from a current app or by creating a new app in PayPal.
  - Create a new PayPal account if you don't already have one. This account will be used for PayPal to credit the payments made by customers.
    - To open a PayPal business account, see <https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register>.
    - To create a PayPal sandbox account see <https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/>.
- (For India) a CSP partner can input their PayU Money account information such as PayU Client ID and password. Partners can find more information on <https://developer.payumoney.com/>.
  - Create a new PayU Money account if you don't already have one. To open a PayU Money account, visit <https://www.payumoney.com/merchant-account/#/>. This account will be used for PayU to credit the payments made by customers.

## <a name="customer-experience-scenarios"></a>Customer experience scenarios

### <a name="new-customer-signup-scenario"></a>New customer signup scenario

- By default, the website is publicly available and shows the partner's catalog on the homepage.
- Customers can now belong to a large number of [customer countries](#customer-countries).
- The focus has been on the European Free Trade Association (EFTA) countries, North America, Japan, India, Australia, and New Zealand regions.
  - This feature uses the regional authorization support in the Partner Center SDK.
- Customers can select an offer from the catalog to purchase.
  - They can add their customer name, address, and domain related information.
- Customers will be directed to the PayPal or PayU (for India) checkout experience. Customers can provide payment using either:
  - Their existing PayPal or PayU (for India) account
  - Funding instruments supported in their country by PayPal or PayU (for India). These may include credit cards, debit cards and bank accounts as applicable.
- A customer tenant is created for this customer. After successful creation of the tenant order, customers are provided the account username, password and subscription details.
  - Customers can save the username and password to stay logged in for further purchases.
  - Each subscription is purchased for a year and customers can renew in the 30 days prior to the subscription end date.

### <a name="view-prior-purchases-scenario"></a>View prior purchases scenario

- Customer signs in with Customer tenant username and password and goes to the **My Orders** section.
- Customers can navigate to the **My Orders** page where they can view purchased subscriptions and make updates if required.
- Customers can navigate to the **My Subscriptions** page where they can view all subscriptions (license-based as well as usage-based), including those maintained in Partner Center.

### <a name="add-seats-to-existing-subscriptions-scenario"></a>Add seats to existing subscriptions scenario

- From the **My Orders** section, customers can add more seats to existing subscriptions. Customers can add more seats anytime during a subscription year.
- Each added seat does not change the end date of the subscription. However, the price of the subscription changes based on the date on which you add the seat, and where that date is in the year. Pricing is prorated on a daily basis to only charge for the remaining days of the year.

### <a name="add-more-subscriptions-scenario"></a>Add more subscriptions scenario

- Customers can buy any number of subscriptions at any time from the **Add subscriptions** section under **My Orders**.
- A customer can select a subscription, add a quantity, and pay to complete the transaction and start using the subscription immediately. If a customer is a pre-approved customer, the subscription is available for use immediately and an invoice will be sent to the customer for payment.

### <a name="renew-subscription-scenario"></a>Renew subscription scenario

- A customer can renew a subscription during the last 30 days prior to the subscription end date.
- This is available only in the last 30 days.
- If not renewed in last 30 days, the subscription will be removed from the list of subscriptions for this Customer tenant.
- You cannot update the quantity during renewal.

### <a name="payments-scenario"></a>Payments scenario

- If the customer is pre-approved for transactions by the admin, the payment experience is not presented for the above scenarios. Instead, the partner can send the invoice for payment to the pre-approved customer.
- For all new purchases, you can add more seats, add subscriptions and renew. A customer can pay a partner using this website through PayPal or PayU (for India).
- This website is integrated with PayPal or PayU (for India) and allows partners to accept payments from their customers. PayPal or PayU (for India) credits this amount in a partner's account. PayPal or PayU (for India) Bank account management is outside of this website and is managed on PayPal.com or PayUmoney.com respectively.
- This is dependent on partners configuring their PayPal orPayU (for India) payment configuration at PayPal.com or PayUmoney.com. Microsoft does not save this information or actual payment transactions resulting from the use of this option.

### <a name="prorated-pricing-scenario"></a>Prorated pricing scenario

- This website supports prorated pricing in cases when customers add more seats to an existing subscription.
- Each subscription expires after one year and cannot be changed after the subscription is purchased.
- The end date of the subscription will not change by adding additional seats. Customers will be charged for the remaining number of days until the end date. For example, if on day one the subscription cost is $365, and you add one more seat on day two, the price for new seat will be $364. If you add one more 10 days later, the price will be $354.