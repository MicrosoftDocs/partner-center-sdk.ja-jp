---
title: カタログ項目を購入する
description: パートナーセンター API を使用してカタログアイテムを購入する方法。
ms.assetid: B9B1B66A-D1AD-44E8-85AA-49D9C2A94BE5
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 50ad9c77773ad5ef2c5c15b1d653ab8d4933bd3e
ms.sourcegitcommit: 45094b6fb1437bca51f97e193ac2957747dbea27
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82124578"
---
# <a name="purchase-catalog-items"></a>カタログ項目を購入する

**適用対象**

- パートナー センター

次のシナリオでは、パートナーセンター API を使用して、カタログから商品を購入するための一般的なプロセスについて説明します。

## <a name="discovery"></a>探索

次のパートナーセンター API モデルを使用して、製品と Sku を選択し、それらの可用性を確認します。

- [Product](product-resources.md#product) -購入可能な商品またはサービスのグループ化構成体。 製品自体は購入可能なの項目ではありません。
- [Sku](product-resources.md#sku) -製品の購入可能な在庫保持ユニット (sku)。 これらは、製品のさまざまな形状を表します。
- [可用性](product-resources.md#availability)-SKU を購入できるようにする構成 (国、通貨、業界セグメントなど)。

カタログから項目を購入するには、次の手順を実行します。

1. 購入する製品と SKU を特定して取得します。

   - [製品の一覧を取得する](get-a-list-of-products.md)
   - [製品 ID を使用して製品を取得する](get-a-product-by-id.md)
   - [製品の Sku の一覧を取得する](get-a-list-of-skus-for-a-product.md)
   - [SKU ID を使用して SKU を取得する](get-a-sku-by-id.md)

2. SKU のインベントリを確認します。 この手順は、 [purchasePrerequisites](product-resources.md#sku)プロパティで**InventoryCheck**値がタグ付けされている sku にのみ必要です。

   - [在庫を確認する](check-inventory.md)

3. [SKU](product-resources.md#sku)の[可用性](product-resources.md#availability)を取得します。 注文を配置するときに、可用性の**Catalogitemid**が必要になります。 この値を取得するには、次の Api のいずれかを使用します。

   - [SKU に使用できる機能の一覧を取得する](get-a-list-of-availabilities-for-a-sku.md)
   - [可用性 ID を使用して可用性を取得する](get-an-availability-by-id.md)

## <a name="order-submission"></a>注文の送信

カタログ項目の順序を提出するには、次の手順を実行します。

1. 購入するカタログアイテムのコレクションを保持する[カート](cart-resources.md)を作成します。 カートを作成すると、同じ[順序](order-resources.md)で一緒に購入できるものに基づいて[カートの品目](cart-resources.md#cartlineitem)が自動的にグループ化されます。

   - [ショッピングカートを作成する](create-a-cart.md)
   - [ショッピングカートを更新する](update-a-cart.md)

2. カートをチェックアウトします。 カートをチェックアウトすると、[注文](order-resources.md)が作成されます。

   - [カートをチェックアウトする](checkout-a-cart.md)

## <a name="get-order-details"></a>注文の詳細を取得する

注文 ID を使用して個々の注文の詳細を取得したり、顧客の注文の一覧を取得したりできます。 注文が送信されてから顧客の注文の一覧に表示されるまでに、最大15分の遅延が発生します。

- 注文 Id を使用して個々の注文の詳細を取得するには、「 [order BY ID を取得](get-an-order-by-id.md)する」を参照してください。

- 顧客 ID を使用して顧客の注文の一覧を取得するには[、「顧客の注文をすべて取得](get-all-of-a-customer-s-orders.md)する」を参照してください。

- 「[顧客と請求サイクルの](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)種類別の注文の一覧を取得する」をご覧ください。[請求サイクルの種類](product-resources.md#billingcycletype)によって顧客の注文の一覧を取得できます。これにより、カタログアイテムの注文 (1 回限りの料金) と年間または月単位または月単位の請求書を個別に一覧表示することができます。

## <a name="lifecycle-management"></a>ライフサイクル管理

パートナーセンターでカタログアイテムのライフサイクルを管理する過程で、カタログアイテムの[権利](entitlement-resources.md)に関する情報を取得し、予約注文 ID を使用して予約の詳細を取得することができます。 これを行う方法の例については、「[権利の取得](get-a-collection-of-entitlements.md)」を参照してください。   

## <a name="invoice-and-reconciliation"></a>請求書と調整

次のシナリオでは、プログラムを使用して顧客の[請求書](invoice-resources.md)を表示し、カタログアイテムの1回限りの料金を含むアカウントの残高と概要を取得する方法について説明します。

### <a name="balance-and-payment"></a>残高と支払い

既定の通貨の種類で、定期的な料金と1回限りの (カタログアイテム) 料金の残高である現在のアカウント残高を取得するには、「[現在のアカウント残高を取得](get-the-reseller-s-current-account-balance.md)する」を参照してください。

### <a name="multi-currency-balance-and-payment"></a>複数通貨の残高と支払い

現在のアカウント残高と、顧客の通貨の種類ごとに1回だけ課金される請求書の概要を含む請求書の概要を取得するには、「[請求書の概要を取得](get-invoice-summaries.md)する」を参照してください。

### <a name="invoices"></a>Invoices

定期的な料金と1回限りの課金を示す請求書のコレクションを取得するには、「[請求書のコレクションを取得](get-a-collection-of-invoices.md)する」を参照してください。 

### <a name="single-invoice"></a>1つの請求書

請求書 ID を使用して特定の請求書を取得するには、「 [ID で請求書を取得](get-invoice-by-id.md)する」を参照してください。  

### <a name="reconciliation"></a>連結

特定の請求書 ID の請求書明細項目の詳細 (調整行項目) のコレクションを取得するには、「[請求書明細項目を取得](get-invoiceline-items.md)する」を参照してください。  

### <a name="download-an-invoice-as-a-pdf"></a>PDF として請求書をダウンロードする

請求書 ID を使用して PDF 形式で請求書明細書を取得するには、「 [invoice ステートメントを取得](get-invoice-statement.md)する」を参照してください。
