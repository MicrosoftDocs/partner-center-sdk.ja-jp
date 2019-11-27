---
title: 商用 marketplace 製品のサブスクリプションを作成する
description: 開発者は、パートナーセンター Api を使用して、商用 marketplace 製品のサブスクリプションを作成および管理できます。
ms.assetid: ''
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 9bdc918387af62eec6abdaf5656e0d8bafb7f2b3
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488652"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>商用 marketplace 製品のサブスクリプションを作成する

適用対象:

* パートナー センター

パートナーセンター API を使用して、商用マーケットプレース製品のサブスクリプションを作成できます。 [市場向けのオファーの一覧を取得](#get-a-list-of-offers-for-a-market)し、商業市場向けサブスクリプションの[注文を作成および送信](#create-and-submit-an-order)してから、[ライセンス認証リンクを取得](#get-activation-link)する必要があります。

また、[ライフサイクル管理を実行](#lifecycle-management)し、これらのサブスクリプションの[請求書を管理](#invoice-and-reconciliation)することもできます。

## <a name="prerequisites"></a>前提条件

* [パートナーセンターの認証](partner-center-authentication.md)資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
* 顧客識別子。 顧客の識別子がない場合: パートナーセンターにサインインし、顧客 の一覧から顧客を選択し、**アカウント** を選択して、 **Microsoft ID**を保存します。

## <a name="get-a-list-of-offers-for-a-market"></a>市場向けプランの一覧を取得する

次のパートナーセンター API モデルを使用して、市場の利用可能なオファーを確認することができます。

* **[Product](product-resources.md#product)** : 購入可能な商品またはサービスのグループ化構成体。 製品自体は購入可能なの項目ではありません。
* **[Sku](product-resources.md#sku)** : 製品の購入可能な在庫保持ユニット (sku)。 これらは、製品のさまざまな形状を表します。
* **[可用性](product-resources.md#availability)** : SKU を購入できるようにする構成 (国、通貨、業界セグメントなど)。

Azure 予約を購入する前に、次の手順を実行します。

1. 購入する製品と SKU を特定して取得します。 製品 ID と SKU ID が既にわかっている場合は、それを選択します。

    * [製品の一覧を取得する](get-a-list-of-products.md)
    * [製品 ID を使用して製品を取得する](get-a-product-by-id.md)
    * [製品の Sku の一覧を取得する](get-a-list-of-skus-for-a-product.md)
    * [SKU ID を使用して SKU を取得する](get-a-sku-by-id.md)

    > [!NOTE]
    > **"Azure"** の**ProductType**プロパティと **"SaaS"** の**SubType**プロパティによって、商業市場製品を特定できます。

2. **InventoryCheck**の前提条件で sku にタグが付けられている場合は、 [sku のインベントリを確認](check-inventory.md)します。

    > [!NOTE]
    > 現時点では、在庫チェックをサポートするか、 **InventoryCheck**の前提条件のタグが付けられている商用 marketplace 製品はありません。

3. SKU の可用性を取得します。 注文を配置するときに、可用性の**Catalogitemid**が必要になります。この場合、次の api を使用して取得できます。

    * [SKU に使用できる機能の一覧を取得する](get-a-list-of-availabilities-for-a-sku.md)
    * [可用性 ID を使用して可用性を取得する](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>注文を作成して送信する

Azure 予約注文を送信するには、次の手順を実行します。

1. 購入するカタログアイテムのコレクションを保持する[カートを作成](create-a-cart.md)します。 [カート](cart-resources.md#cart)を作成すると、同じ[順序](order-resources.md#order)で一緒に購入できるものに基づいて[カートの品目](cart-resources.md#cartlineitem)が自動的にグループ化されます。 ([カートを更新](update-a-cart.md)することもできます)。
2. [カート](checkout-a-cart.md)をチェックアウトすると、[注文](order-resources.md#order)が作成されます。

### <a name="get-order-details"></a>注文の詳細を取得する

[注文 ID を使用して、個々の注文の詳細を取得](get-an-order-by-id.md)できます。 また、[特定の顧客のすべての注文の一覧を取得](get-all-of-a-customer-s-orders.md)することもできます。

> [!NOTE]
> 注文が送信されると、その顧客の注文リストに注文が表示されるまでに最大15分の遅延が発生します。

## <a name="get-activation-link"></a>アクティブ化リンクの取得

パートナーまたは顧客は、Azure にマークされた場所製品のサブスクリプションをアクティブ化する必要があります。 [注文明細項目を使用してアクティブ化リンクを取得](get-activation-link-by-order-line-item.md)できます。 また、 [ID でサブスクリプションを取得](get-a-subscription-by-id.md)し、その**Links**プロパティを列挙してアクティベーションリンクを作成することもできます。

## <a name="lifecycle-management"></a>ライフサイクルの管理

次の方法を使用して、商用 marketplace 製品に対するサブスクリプションのライフサイクルを管理できます。

* [商用 marketplace サブスクリプションをキャンセルする](cancel-an-azure-marketplace-subscription.md)
* [商用 marketplace サブスクリプションの autorenew を有効または無効にする](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>数量管理

商用 marketplace サブスクリプションの数量は、関連付けられている[SKU](product-resources.md#sku)で定義されている制限内である必要があります ( **Minimumquantity**属性と**maximumquantity**属性を参照してください)。 商用 marketplace サブスクリプションの数量を更新するには、次の方法を使用します。

* [サブスクリプションの数量を変更する](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>請求書と調整

次の方法を使用して、顧客の[請求書](invoice-resources.md)(商用 marketplace 製品へのサブスクリプションの請求を含む) を管理できます。

* [請求書を取得する商用マーケットプレースの従量課金明細項目](get-invoice-billed-consumption-lineitems.md)
* [請求書の推定リンクの取得](get-invoice-estimate-links.md)
* [Invoice 未請求商業市場消費量の品目を取得する](get-invoice-unbilled-consumption-lineitems.md)
* [Invoice 未請求調整の品目を取得する](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>統合サンドボックスアカウントを使用してテストする

運用環境では、商用 marketplace SaaS 製品へのサブスクリプションを作成した後で、パートナーセンターからパーソナライズされたアクティベーションリンクを取得し、発行者のサイトにアクセスしてセットアッププロセスを完了する必要があります。 サブスクリプションの課金は、セットアップの完了後にのみ開始されます。

CSP サンドボックス環境では、Isv との統合はありません。 パートナーセンターからライセンス認証リンクを取得しようとすると、ダミーリンクが返されます。 このダミーリンクを使用して、発行元のサイトでセットアッププロセスを完了することはできません。 統合サンドボックスアカウントを使用して、商用 marketplace SaaS 製品へのサブスクリプションの課金をテストするには、次の方法を使用してサブスクリプションをアクティブ化します。 アクティブ化が成功すると、サブスクリプションの課金が開始されます。

* [商用 marketplace 製品のサンドボックスサブスクリプションをアクティブ化する](activate-sandbox-subscription-azure-marketplace-products.md)

