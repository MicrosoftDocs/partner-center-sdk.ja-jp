---
title: Make a one-time purchase
description: How to make a one-time purchase of software and reservation products such as software subscriptions, perpetual software, and Azure Reserved Virtual Machine (VM) Instances, using the Partner Center API.
ms.date: 10/09/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 088f60bb249985a01d955aa53fc1ab7fb995f759
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488372"
---
# <a name="make-a-one-time-purchase"></a>Make a one-time purchase

**Applies To**

- パートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

How to make a one-time purchase of software and reservation products such as software subscriptions, perpetual software, and Azure Reserved Virtual Machine (VM) Instances, using the Partner Center API.

> [!NOTE]  
> Software subscriptions are not available in the following markets:  
>  
> | Unavailable Markets            | &nbsp;                            | &nbsp;                                   |
> |--------------------------------|-----------------------------------|------------------------------------------|
> | オーランド諸島                  | グリーンランド                         | パプアニューギニア                         |
> | 米領サモア                 | グレナダ                           | ピトケアン島                         |
> | アンドラ                        | グアドループ                        | レユニオン                                  |
> | アンギラ                       | グアム                              | ロシア連邦                       |
> | 南極                     | ガーンジー島                          | サバ島                                     |
> | アンティグア・バーブーダ            | ギニア                            | サン・バルテルミー                         |
> | アルバ                          | ギニアビサウ                     | セントルシア                              |
> | ベナン                          | ガイアナ                            | サンマルタン島                             |
> | ブータン                         | ハイチ                             | サンピエール・ミクロン                |
> | ボネール島                        | ハード・マクドナルド諸島 | セントビンセントおよびグレナディーン諸島         |
> | ブーベ島                  | マン島                       | サモア                                    |
> | ブラジル                         | ヤンマイエン島                         | サンマリノ                               |
> | 英領インド洋地域 | ジャージー島                            | サントメ・プリンシペ                    |
> | 英領バージン諸島         | キリバス                          | セーシェル                               |
> | ブルキナファソ                   | コソボ                            | シエラレオネ                             |
> | ブルンジ                        | ラオス                              | シント・ユースタティウス島                           |
> | カンボジア                       | レソト                           | シント・マールテン島                             |
> | 中央アフリカ共和国       | リベリア                           | ソロモン諸島                          |
> | チャド                           | マダガスカル                        | ソマリア                                  |
> | 中国                          | マラウイ                            | サウスジョージア・サウスサンドウィッチ諸島 |
> | クリスマス島               | モルディブ                          | 南スーダン                              |
> | ココス諸島        | マリ                              | セントヘレナ、アセンションおよびトリスタンダクーニャ   |
> | コモロ                        | マーシャル諸島                  | スリナム                                 |
> | コンゴ共和国                          | マルチニーク島                        | スバールバル諸島                                 |
> | コンゴ民主共和国                    | モーリタニア                        | スワジランド                                |
> | クック諸島                   | マイヨット島                           | ティモール・レステ                              |
> | ジブチ                       | ミクロネシア                        | トーゴ                                     |
> | ドミニカ国                       | モンセラット                        | トケラウ諸島                                  |
> | 赤道ギニア              | モザンビーク                        | トンガ                                    |
> | エリトリア                        | ミャンマー                           | タークス・カイコス諸島                 |
> | フォークランド諸島               | ナウル                             | ツバル                                   |
> | フランス領ギアナ                  | ニューカレドニア                     | 合衆国領有小離島                    |
> | フランス領ポリネシア               | ニジェール                             | バヌアツ                                  |
> | 仏領極南諸島    | ニウエ                              | バチカン市国                             |
> | ガボン                          | ノーフォーク島                    | ワリス・フテュナ諸島                        |
> | ガンビア                         | 北マリアナ諸島          | イエメン                                    |
> | ジブラルタル                      | パラオ                             | &nbsp;                                   |
>  
&nbsp;
> [!NOTE]
> To purchase perpetual software, you must have been previously qualified. Contact support for more information.

## <a name="prerequisites"></a>前提条件

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A customer identifier. If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.

## <a name="making-a-one-time-purchase"></a>Making a one-time purchase

To make a one-time purchase, use the following steps:

1. [Enablement](#enablement) - (Azure Reserved VM Instance only) Register an active CSP Azure subscription to enable it for purchasing any reservation product.
2. [Discovery](#discovery) - Find and select the products and SKUs you want to purchase and check their availability.
3. [Order submission](#order-submission) - Create a shopping cart with the items in your order and submit it.
4. [Get order details](#get-order-details) - Review the details of an order, all the orders for a customer, or view orders by billing cycle type.

After you have made your one-time purchase, the following scenarios show you how to manage the lifecycle of your products by getting information about your entitlements, and how to retrieve balance statements, invoices, and invoice summaries.

- [Lifecycle management](#lifecycle-management)
- [Invoice and reconciliation](#invoice-and-reconciliation)

## <a name="enablement"></a>有効化

Once you have identified the active subscription that you want to add the Azure Reserved VM Instance to, you must register the subscription so that it is enabled. To register an existing [Subscription](subscription-resources.md) resource so that it is enabled, see [Register a subscription](register-a-subscription.md).

After registering your subscription, you should confirm that the registration process is completed by checking the registration status. To do this, see [Get subscription registration status](get-subscription-registration-status.md).

## <a name="discovery"></a>情報表示

Once the subscription is enabled, you're ready to select products and SKUs and check their availability using the following Partner Center API models:

- [Product](product-resources.md#product) - A grouping construct for purchasable goods or services. A product by itself is not a purchasable item.
- [SKU](product-resources.md#sku) - A purchasable Stock Keeping Unit (SKU) under a product. These represent the different shapes of the product.
- [Availability](product-resources.md#availability) - A configuration in which a SKU is available for purchase (such as country, currency and industry segment).

Before making a one-time purchase, complete the following steps:

1. Identify and retrieve the Product and SKU that you want to purchase. You can do this by listing the products and SKUs first, or If you already know the IDs of the product and SKU, selecting them.

    - [Get a list of products](get-a-list-of-products.md)
    - [Get a product using the product ID](get-a-product-by-id.md)
    - [Get a list of SKUs for a product](get-a-list-of-skus-for-a-product.md)
    - [Get a SKU using the SKU ID](get-a-sku-by-id.md)

2. Check the inventory for a SKU. This step is only needed for SKUs that are tagged with an **InventoryCheck** prerequisite.

    - [Check Inventory](check-inventory.md)

3. Retrieve the [availability](product-resources.md#availability) for the [SKU](product-resources.md#sku). You will need the **CatalogItemId** of the availability when placing the order. To get this value, use one of the following APIs:

    - [Get a list of availabilities for a SKU](get-a-list-of-availabilities-for-a-sku.md)
    - [Get an availability using the availability ID](get-an-availability-by-id.md)  

## <a name="order-submission"></a>Order submission

To submit your order, do the following:

1. Create a cart to hold the collection of catalog items that you intend to buy. When you create a [Cart](cart-resources.md), the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [Order](order-resources.md).

    - [Create a shopping cart](create-a-cart.md)
    - [Update a shopping cart](update-a-cart.md)

2. Check out the cart. Checking out a cart results in the creation of an [Order](order-resources.md).

    - [Checkout the cart](checkout-a-cart.md)

## <a name="get-order-details"></a>Get order details

Once you have created your order, you can retrieve the details of an individual order using the order ID, or get a list of orders for a customer. Note that there is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a list of a customer's orders.

- To get the details of an individual order using the order ID. See, [Get an order by ID](get-an-order-by-id.md).

- To get a list of orders for a customer using the customer ID. See, [Get all of a customer's orders](get-all-of-a-customer-s-orders.md).

- To get a list of orders for a customer by [billing cycle type](product-resources.md#billingcycletype) allowing you to list orders (one-time charges) and annual or monthly billed orders separately. See, [Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>ライフサイクルの管理

As part of managing the lifecycle of your one-time purchases in Partner Center, you can retrieve information about your [Entitlements](entitlement-resources.md), and get reservation details using the reservation order ID. For examples of how to do this, see [Get entitlements](get-a-collection-of-entitlements.md).

## <a name="invoice-and-reconciliation"></a>Invoice and reconciliation

The following scenarios show you how to programmatically view your customer's [invoices](invoice-resources.md), and get your account balances and summaries that include one-time charges.  

**Balance and payment** To get current account balance in your default currency type that is a balance of both recurring and one-time charges, see [Get your current account balance](get-the-reseller-s-current-account-balance.md)

**Multi-currency balance and payment** To get your current account balance and a collection of invoice summaries containing an invoice summary with both recurring and one-time charges for each of your customer's currency types, see [Get invoice summaries](get-invoice-summaries.md).

**Invoices** To get a collection of invoices that show both recurring and one time charges, see [Get a collection of invoices](get-a-collection-of-invoices.md).

**Single Invoice** To retrieve a specific invoice using the invoice ID, see [Get an invoice by ID](get-invoice-by-id.md).  

**Reconciliation** To get a collection of invoice line item details (Reconciliation line items) for a specific invoice ID, see [Get invoice line items](get-invoiceline-items.md).  

**Download an invoice as a PDF** To retrieve an invoice statement in PDF form using an invoice ID, see [Get an invoice statement](get-invoice-statement.md).
