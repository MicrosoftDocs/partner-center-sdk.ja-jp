---
title: Purchase catalog items
description: How to purchase catalog items using the Partner Center API.
ms.assetid: B9B1B66A-D1AD-44E8-85AA-49D9C2A94BE5
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ff4f04bc53f96e6e7670922093bca830456de921
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486742"
---
# <a name="purchase-catalog-items"></a>Purchase catalog items


**Applies To**

- パートナー センター


The following scenario demonstrates the generic process for purchasing items from the catalog by using the Partner Center API.


## <a name="span-iddiscoveryspan-iddiscoveryspan-iddiscoverydiscovery"></a><span id="Discovery"/><span id="discovery"/><span id="DISCOVERY"/>Discovery

Select products and SKUs and check their availability using the following Partner Center API models: 

- [Product](product-resources.md#product) - A grouping construct for purchasable goods or services. A product by itself is not a purchasable item.
- [SKU](product-resources.md#sku) - A purchasable Stock Keeping Unit (SKU) under a product. These represent the different shapes of the product.
- [Availability](product-resources.md#availability) - A configuration in which a SKU is available for purchase (such as country, currency and industry segment).

To purchase an item from the catalog, complete the following steps:

1.  Identify and retrieve the Product and SKU that you want to purchase.

    - [Get a list of products](get-a-list-of-products.md)
    - [Get a product using the product ID](get-a-product-by-id.md)
    - [Get a list of SKUs for a product](get-a-list-of-skus-for-a-product.md)
    - [Get a SKU using the SKU ID](get-a-sku-by-id.md)

2.  Check the inventory for a SKU. This step is only needed for SKUs that are tagged with an **InventoryCheck** value in the [purchasePrerequisites](product-resources.md#sku) property.

    - [Check Inventory](check-inventory.md) 

3.  Retrieve the [availability](product-resources.md#availability) for the [SKU](product-resources.md#sku). You will need the **CatalogItemId** of the availability when placing the order. To get this value, use one of the following APIs: 

    - [Get a list of availabilities for a SKU](get-a-list-of-availabilities-for-a-sku.md)
    - [Get an availability using the availability ID](get-an-availability-by-id.md)


## <a name="span-idorder_submissionspan-idorder_submissionspan-idorder_submissionorder-submission"></a><span id="Order_submission"/><span id="order_submission"/><span id="ORDER_SUBMISSION"/>Order submission

To submit your catalog item order, do the following:

1.  Create a [Cart](cart-resources.md) to hold the collection of catalog items that you intend to buy. When you create a cart, the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [Order](order-resources.md).

    - [Create a shopping cart](create-a-cart.md)
    - [Update a shopping cart](update-a-cart.md)

2.  Check out the cart. Checking out a cart results in the creation of an [Order](order-resources.md). 

    - [Checkout the cart](checkout-a-cart.md)

## <a name="span-idget_order_detailsspan-idget_order_detailsspan-idget_order_detailsget-order-details"></a><span id="Get_order_details"/><span id="get_order_details"/><span id="GET_ORDER_DETAILS"/>Get order details



You can retrieve the details of an individual order using the order ID, or get a list of orders for a customer. Note that there is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a list of a customer's orders. 

- See [Get an order by ID](get-an-order-by-id.md) to get the details of an individual order using the order IDs.

- See [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) to get a list of orders for a customer using the customer ID.      

-  See [Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) to get a list of orders for a customer by [billing cycle type](product-resources.md#billingcycletype) allowing you to list catalog item orders (one-time charges) and annual or monthly billed orders separately. 

## <a name="span-idlifecycle_managementspan-idlifecycle_managementspan-idlifecycle_managementlifecycle-management"></a><span id="Lifecycle_management"/><span id="lifecycle_management"/><span id="LIFECYCLE_MANAGEMENT"/>Lifecycle management



As part of managing the lifecycle of your catalog items in Partner Center, you can retrieve information about your catalog item [Entitlements](entitlement-resources.md), and get reservation details using the reservation order ID. For examples of how to do this, see [Get entitlements](get-a-collection-of-entitlements.md).   

## <a name="span-idinvoice_and_reconciliationspan-idinvoice_and_reconciliationspan-idinvoice_and_reconciliationinvoice-and-reconciliation"></a><span id="Invoice_and_reconciliation"/><span id="invoice_and_reconciliation"/><span id="INVOICE_AND_RECONCILIATION"/>Invoice and reconciliation



The following scenarios show you how to programmatically view your customer's [invoices](invoice-resources.md), and get your account balances and summaries that include one-time charges for catalog items.  

**Balance and payment**    
To get current account balance in your default currency type that is a balance of both recurring and one-time (catalog item) charges, see [Get your current account balance](get-the-reseller-s-current-account-balance.md)

**Multi-currency balance and payment**    
To get your current account balance and a collection of invoice summaries containing an invoice summary with both recurring and one-time charges for each of your customer's currency types, see [Get invoice summaries](get-invoice-summaries.md).

**Invoices**    
To get a collection of invoices that show both recurring and one-time charges, see [Get a collection of invoices](get-a-collection-of-invoices.md). 

**Single Invoice**    
To retrieve a specific invoice using the invoice ID, see [Get an invoice by ID](get-invoice-by-id.md).  

**Reconciliation**    
To get a collection of invoice line item details (Reconciliation line items) for a specific invoice ID, see [Get invoice line items](get-invoiceline-items.md).  

**Download an invoice as a PDF**    
To retrieve an invoice statement in PDF form using an invoice ID, see [Get an invoice statement](get-invoice-statement.md).

