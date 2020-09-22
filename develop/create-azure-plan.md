---
title: Azure プランを作成する
description: 開発者は、パートナーセンター Api を使用して、Azure プランをプログラムによって購入、作成、管理できます。
ms.date: 01/02/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: mowrim
ms.author: mowrim
ms.openlocfilehash: 372b94ac7217899ca560cf943bf11a7e8906872d
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927346"
---
# <a name="create-an-azure-plan"></a>Azure プランを作成する

**適用対象:**

* パートナー センター

パートナーセンター Api を使用して、Azure プランの購入、作成、管理を行うことができます。 このプロセスは、Microsoft Azure (0145P) サブスクリプションの作成と似ています。 [Azure プランのカタログアイテムを取得](#get-the-catalog-item-for-azure-plan)し、[注文を作成して送信](#create-and-submit-an-order)する必要があります。

## <a name="prerequisites"></a>前提条件

* [パートナーセンターの認証](partner-center-authentication.md) 資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
* 顧客 ID。 顧客の識別子がない場合は、「 [顧客の一覧を取得する](get-a-list-of-customers.md)」の手順に従います。 または、パートナーセンターにサインインして、顧客の一覧から顧客を選択し、[ **アカウント**] を選択して、 **Microsoft ID**を保存します。
* [お客様が Microsoft カスタマーアグリーメントに同意](/partner-center/confirm-customer-agreement)したことを確認します。

## <a name="get-the-catalog-item-for-azure-plan"></a>Azure プランのカタログアイテムを取得する

顧客の Azure プランを作成するには、対応するカタログアイテムを取得する必要があります。 既存のパートナーセンターカタログ Api と次のリソースモデルを使用して、カタログアイテムを取得できます。

* **[Product](product-resources.md#product)**: 購入可能な商品またはサービスのグループ化構成体。 製品自体は購入可能なの項目ではありません。
* **[Sku](product-resources.md#sku)**: 製品の購入可能な在庫保持ユニット (sku)。 Sku は、製品のさまざまな形状を表します。
* **[可用性](product-resources.md#availability)**: SKU を購入できるようにする構成 (国、通貨、業界セグメントなど)。

Azure プランのカタログアイテムを取得するには、次の手順を実行します。

1. Azure プランの *製品* 識別子を特定して取得します。 「 [製品の一覧を取得する](get-a-list-of-products.md) 」の手順に従って、 **Targetview** を **microsoftazure.mobileengagement**として指定します。 (Azure プランの *製品* 識別子が既にわかっている場合は、「製品 [id を使用して製品を取得](get-a-product-by-id.md) する」の手順に従うことができます)。

2. Azure プランの製品から **SKU** を取得します。 「 [製品の sku の一覧を取得する](get-a-list-of-skus-for-a-product.md)」の手順に従います。 Azure プランの SKU 識別子が既にわかっている場合は、「sku [id を使用して sku を取得](get-a-sku-by-id.md) する」の手順に従ってください。

3. Azure プランの SKU から **可用性** を取得します。 「 [SKU に利用できる機能の一覧を取得する](get-a-list-of-availabilities-for-a-sku.md)」の手順に従います。 必要な可用性の識別子が既にわかっている場合は、「可用性 [ID を使用した可用性の取得](get-an-availability-by-id.md) 」の手順に従ってください。 *Azure プランの可用性の **Catalogitemid** プロパティの値をメモしておいてください。注文を作成するには、この値が必要になります。*

## <a name="create-and-submit-an-order"></a>注文を作成して送信する

Azure プランの注文を送信するには、次の手順を実行します。

1. 購入するカタログアイテムのコレクションを保持する[カートを作成](create-a-cart.md)します。 [カート](cart-resources.md#cart)を作成すると、同じ[順序](order-resources.md#order)で一緒に購入できるものに基づいて[カートの品目](cart-resources.md#cartlineitem)が自動的にグループ化されます。 ( [カートを更新](update-a-cart.md)することもできます)。

2. [カート](checkout-a-cart.md)をチェックアウトすると、 [注文](order-resources.md#order)が作成されます。

## <a name="get-order-details"></a>注文の詳細を取得する

[注文 ID を使用して、個々の注文の詳細を取得](get-an-order-by-id.md)できます。 また、 [特定の顧客のすべての注文の一覧を取得](get-all-of-a-customer-s-orders.md)することもできます。

>[!NOTE]
>注文が送信されると、その顧客の注文リストに注文が表示されるまでに最大15分の遅延が発生します。

## <a name="manage-azure-plans"></a>Azure プランの管理

注文が正常に処理されると、Azure プランのパートナーセンターの **サブスクリプション** リソースが作成されます。 パートナーセンターの **サブスクリプション** リソースを管理して Azure プランを管理するには、次の方法を使用できます。

* [顧客のサブスクリプションを取得する](get-all-of-a-customer-s-subscriptions.md)
* [注文ごとにサブスクリプションの一覧を取得する](get-a-list-of-subscriptions-by-order.md)

Azure プランがパートナーセンターで作成されると、対応する Azure usage サブスクリプションも Azure に作成されます。 Azure Portal と Azure Api を使用して、同じ Azure プランで追加の Azure 使用サブスクリプションを作成することもできます。 Azure プランに関連付けられているすべての Azure 使用サブスクリプションの id を取得するには、「[パートナーセンターのサブスクリプションに対する azure の権利の一覧を取得](get-a-list-of-azure-entitlements-for-subscription.md)する」の手順に従ってください。

## <a name="lifecycle-management"></a>ライフサイクル管理

既存の Azure プランを中断するには、「 [サブスクリプションを中断](suspend-a-subscription.md)する」の手順に従ってください。

*既存の Azure プランに関連付けられているアクティブな使用状況アセット (Azure の使用サブスクリプションや Azure の予約を含む) がなくなった場合に限り、そのプランを中断できます。*

Azure の使用サブスクリプションを無効にする方法の詳細については、「 [サブスクリプションライフサイクル管理での AZURE API](/rest/api/resources/subscriptions)」を参照してください。

既存の Azure 予約を削除するには、 [予約を取り消す](/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation)必要があります。
Azure プランを中断した後、再アクティブ化することができます。

Azure プランを再アクティブ化する方法の詳細については、「中断され[たサブスクリプションの再アクティブ化](reactivate-a-suspended-a-subscription.md)」を参照してください。

## <a name="transition-existing-csp-offers-to-azure-plan"></a>既存の CSP オファーを Azure プランに移行する

Microsoft Azure (0145P) サブスクリプションを使用して、既存の顧客の Azure プランを作成することはできません。 ただし、パートナーセンター内の CSP プログラムの新しいコマースエクスペリエンスでは、azure [プランの既存の csp から azure サービスにお客様を移行](/partner-center/azure-plan-transition) することができます。 既存の顧客を移行するには、product upgrade Api を使用して次の手順を実行します。

* [お客様が Azure プランへの移行の対象であるかどうかを確認する](get-eligibility-for-product-upgrade.md)
* [顧客の製品のアップグレードを開始する](create-product-upgrade-entity.md)
* [製品のアップグレードの状態を確認する](get-product-upgrade-status.md)

## <a name="azure-spending"></a>Azure 利用状況

次の方法を使用して、使用状況の概要と詳細な使用状況レコードを照会することで、 [Azure](azure-spending.md) の使用量を追跡できます。

* [パートナーの使用量に関する概要を取得する](get-a-partner-usage-summary.md)
* [パートナーのすべての顧客の使用状況レコードを取得する](get-a-customer-s-usage-records.md)
* [顧客の使用状況の概要を取得する](get-a-customer-usage-summary.md)
* [顧客のすべてのサブスクリプション使用状況レコードを取得する](get-a-customer-subscription-s-usage-records.md)
* [サブスクリプションの使用状況の概要を取得する](get-a-customer-subscription-usage-summary.md)
* [サブスクリプションの使用状況データをリソースごとに取得する](get-a-customer-subscription-resource-usage-records.md)
* [サブスクリプションの使用状況データをメーターごとに取得する](get-a-customer-subscription-meter-usage-records.md)
* [メーター使用状況レコードのリソースを取得する](meter-usage-resources.md)
* [リソース使用状況レコードのリソースを取得する](resource-usage-resources.md)

次の方法を使用して、顧客の使用量の予算を設定および管理することもできます。

* [顧客の使用予算を取得する](get-a-customer-s-usage-spending-budget.md)
* [顧客の使用予算を更新する](update-a-customer-s-usage-spending-budget.md)

## <a name="invoice-and-reconciliation"></a>請求書と調整

次の方法を使用して、請求書と調整データを管理できます。

* [請求書のコレクションを取得する](get-a-collection-of-invoices.md)
* [請求書の推定リンクを取得する](get-invoice-estimate-links.md)
* [請求書を ID で取得する](get-invoice-by-id.md)
* [請求明細書を取得する](get-invoice-statement.md)
* [請求書の概要を取得する](get-invoice-summaries.md)
* [請求書の課金明細を取得する](get-invoice-billed-consumption-lineitems.md)
* [請求書の未課金明細を取得する](get-invoice-unbilled-consumption-lineitems.md)
* [品目の請求書の取得](get-invoiceline-items.md)
* [請求書の未課金照合明細を取得する](get-invoice-unbilled-recon-lineitems.md)
