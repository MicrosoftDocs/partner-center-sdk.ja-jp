---
title: シナリオ
description: このセクションでは、クラウドソリューションプロバイダープログラムのパートナーがパートナーセンター API を使用して、顧客アカウント、パートナーアカウント、注文、サブスクリプション、サポート、および課金をプログラムで管理する方法について説明します。
ms.assetid: D278B9D1-D5B9-4FAD-89D8-44244715D6C9
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ff5632f0826375c973779f5135696087b3da9621
ms.sourcegitcommit: 7e5e3590931010eb0e0fef3e7f6d5d7d084a69ba
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74995267"
---
# <a name="scenarios"></a>シナリオ

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

このセクションでは、クラウドソリューションプロバイダープログラムのパートナーがパートナーセンター API を使用して、顧客アカウント、パートナーアカウント、注文、サブスクリプション、サポート、および課金をプログラムで管理する方法について説明します。

さまざまな機能を含むパートナーセンターの異なるバージョンがあることに注意してください。 すべてのシナリオがパートナーセンターのすべてのバージョンでサポートされているわけではありません。 詳細については、「 [Microsoft National Cloud のパートナーセンター向けの開発](developing-for-partner-center-for-microsoft-national-cloud.md)」を参照してください。

## <a name="scenarios-supported-by-the-partner-center-sdk"></a>パートナーセンター SDK でサポートされるシナリオ

次のシナリオはすべて、3つの異なる方法で完了できます。

- [パートナーセンター](https://go.microsoft.com/fwlink/p/?LinkId=620294)のダッシュボードで手動で行います。
- パートナーセンターで管理されている API をプログラムで使用する。
- パートナーセンターの REST API を使用したプログラム。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr>
<td><p><a href="usage-analytics.md">分析</a></p></td>
<td><p>分析の取得</p>
<ul>
<li><p><a href="partner-center-analytics-resources.md">パートナー センターの分析 - リソース</a></p></li>
<li><p><a href="get-all-azure-usage-analytics.md">Azure の使用量分析情報をすべて取得する</a></p></li>
<li><p><a href="get-all-indirect-resellers-analytics.md">間接顧客の分析情報をすべて取得する</a></p></li>
<li><p><a href="get-all-referrals-analytics.md">紹介の分析情報をすべて取得する</a></p></li>
<li><p><a href="get-all-search-analytics.md">検索の分析情報をすべて取得する</a></p></li>
<li><p><a href="get-all-subscription-analytics.md">サブスクリプションの分析情報をすべて取得する</a></p></li>
<li><p><a href="get-subscription-analytics-by-search-query.md">検索クエリでフィルター処理されたサブスクリプションの分析情報を取得する</a></p></li>
<li><p><a href="get-subscription-analytics-grouped-by-dates-or-terms.md">日付またはご契約条件でグループ化されたサブスクリプションの分析情報を取得する</a></p></li>
<li><p><a href="get-licenses-deployment-information.md">ライセンスのデプロイ情報を取得する</a></p></li>
<li><p><a href="get-licenses-usage-information.md">ライセンスの使用情報を取得する</a></p></li>
<li><p><a href="get-customer-licenses-deployment-information.md">顧客ライセンスのデプロイ情報を取得する</a></p></li>
<li><p><a href="get-customer-licenses-usage-information.md">顧客ライセンスの使用情報を取得する</a></p></li>
<li><p><a href="get-partner-licenses-deployment-information.md">パートナー ライセンスのデプロイ情報を取得する</a></p></li>
<li><p><a href="get-partner-licenses-usage-information.md">パートナー ライセンスの使用情報を取得する</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="device-deployment.md">デバイスの展開</a></p></td>
<td><p>構成ポリシー</p>
<p>デバイス構成ポリシーを追加、削除、更新、および取得します。</p>
<ul>
<li><p><a href="create-a-new-configuration-policy-for-the-specified-customer.md">指定された顧客の新しい構成ポリシーを作成する</a></p></li>
<li><p><a href="delete-a-configuration-policy-for-the-specified-customer.md">指定された顧客の構成ポリシーを削除する</a></p></li>
<li><p><a href="get-a-list-of-a-customer-s-policies.md">顧客&#39;のポリシーの一覧を取得する</a></p></li>
<li><p><a href="retrieve-a-customer-s-configuration-policy.md">顧客&#39;の構成ポリシーを取得する</a></p></li>
<li><p><a href="update-a-configuration-policy-for-the-specified-customer.md">指定された顧客の構成ポリシーを更新する</a></p></li>
</ul>
<p>[デバイス]</p>
<p>デバイスのバッチとデバイスのメタデータを操作してアップロードします。</p>
<ul>
<li><p><a href="get-the-status-of-a-device-batch-upload.md">デバイスのバッチ アップロードの状態を取得する</a></p></li>
<li><p><a href="get-the-list-of-device-batches-for-the-specified-customer.md">指定された顧客のデバイス バッチの一覧を取得する</a></p></li>
<li><p><a href="get-a-list-of-devices-for-the-specified-batch-and-customer.md">指定されたバッチと顧客のデバイスの一覧を取得する</a></p></li>
<li><p><a href="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer.md">デバイスの一覧をアップロードして指定された顧客の新しいバッチを作成する</a></p></li>
<li><p><a href="upload-a-list-of-devices-for-the-specified-customer.md">デバイスの一覧を指定された顧客の既存のバッチにアップロードする</a></p></li>
<li><p><a href="delete-a-device-for-the-specified-customer.md">指定された顧客のデバイスを削除する</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-profiles-and-information.md">アカウントとプロファイルを管理する</a></p></td>
<td><p>アカウントとプロファイルを操作する</p>
<ul>
<li><p><a href="get-legal-business-profile.md">パートナーの法的ビジネス プロファイルを取得する</a></p></li>
<li><p><a href="get-an-organization-profile.md">組織プロファイルを取得する</a></p></li>
<li><p><a href="get-partner-billing-profile.md">パートナーの請求プロファイルを取得する</a></p></li>
<li><p><a href="get-partner-network-profile.md">Microsoft Partner Network プロファイルを取得する</a></p></li>
<li><p><a href="get-support-profile.md">サポート プロファイルを取得する</a></p></li>
<li><p><a href="update-legal-business-profile.md">パートナーの法的ビジネス プロファイルを更新する</a></p></li>
<li><p><a href="update-partner-billing-profile.md">パートナーの請求プロファイルを更新する</a></p></li>
<li><p><a href="update-support-profile.md">サポート プロファイルを更新する</a></p></li>
<li><p><a href="update-an-organization-profile.md">組織プロファイルを更新する</a></p></li>
<li><p><a href="get-partner-by-mpn-id.md">パートナーの MPN ID を検証する</a></p></li>
<li><p><a href="get-all-subscriptions-by-partner.md">パートナー MPN ID&#39;で顧客のサブスクリプションを取得する</a></p></li>
<li><p><a href="get-customers-of-an-indirect-reseller.md">間接リセラーの顧客を取得する</a></p></li>
<li><p><a href="get-indirect-resellers-of-a-customer.md">顧客の間接リセラーを取得する</a></p></li>
<li><p><a href="retrieve-a-list-of-indirect-resellers.md">間接リセラーの一覧を取得する</a></p></li>
</ul></td>
</tr>
<tr>
<td>
<p><a href="manage-billing.md">請求を管理する</a></p></td>
<td><p>Billing cycle</p>
<ul>
<li><p><a href="change-the-billing-cycle.md">請求サイクルを変更する</a></p></li>
</ul>
<p>Azure の料金と使用率のレコード</p>
<ul>
<li><p><a href="get-prices-for-microsoft-azure.md">Microsoft Azure の価格を取得する</a></p></li>
<li><p><a href="get-a-customer-s-utilization-record-for-azure.md">Azure の顧客&#39;の使用状況レコードを取得する</a></p></li>
</ul>
<p>請求書</p>
<ul>
<li><p><a href="get-a-collection-of-invoices.md">請求書のコレクションを取得する</a></p></li>
<li><p><a href="get-invoice-estimate-links.md">請求書の推定リンクを取得する</a></p></li>
<li><p><a href="get-invoice-billed-consumption-lineitems.md">請求書を取得する商用マーケットプレースの従量課金明細項目</a></p></li>
<li><p><a href="get-invoice-by-id.md">請求書を ID で取得する</a></p></li>
<li><p><a href="get-invoiceline-items.md">請求書の品目を取得する</a></p></li>
<li><p><a href="get-invoice-receipt-statement.md">請求書の領収書を取得する</a></p></li>
<li><p><a href="get-invoice-statement.md">請求明細書を取得する</a></p></li>
<li><p><a href="get-invoice-summaries.md">請求書の概要を取得する</a></p></li>
<li><p><a href="get-invoice-unbilled-consumption-lineitems.md">Invoice 未請求商業市場消費量の品目を取得する</a></p></li>
<li><p><a href="get-invoice-unbilled-recon-lineitems.md">請求書の未課金照合明細を取得する</a></p></li>
<li><p><a href="get-the-reseller-s-current-account-balance.md">パートナー&#39;の現在のアカウント残高を取得する</a></p></li>
</ul>
<p>Azure の支出予算</p>
<ul>
<li><p><a href="get-all-monthly-usage-records-for-a-subscription.md">サブスクリプションの使用状況データの取得</a></p></li>
<li><p><a href="get-a-customer-usage-summary.md">すべての顧客&#39;のサブスクリプションの使用状況の概要を取得する</a></p></li>
</ul>
<p>サービスのコスト</p>
<ul>
<li><p><a href="get-a-customer-s-service-costs-summary.md">顧客&#39;のサービスコストの概要を取得する</a></p></li>
<li><p><a href="get-a-customer-s-service-costs-line-items.md">顧客&#39;のサービスコストの明細項目を取得する</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-customers.md">顧客のアカウントを管理する</a></p></td>
<td><p>顧客の作成</p>
<ul>
<li><p><a href="create-a-customer.md">顧客を作成する</a></p></li>
<li><p><a href="create-a-customer-for-an-indirect-reseller.md">間接リセラーの顧客を作成する</a></p></li>
<li><p><a href="request-reseller-relationship.md">関係要求 URL を取得する</a></p></li>
<li><p><a href="remove-a-reseller-relationship-with-a-customer.md">顧客との再販業者関係の削除</a></p></li> 
</ul>
<p>顧客を検索する</p>
<ul>
<li><p><a href="get-a-customer-by-id.md">ID で顧客を取得する</a></p></li>
<li><p><a href="get-a-customer-by-name.md">検索フィールドによってフィルター処理された顧客の一覧を取得する</a></p></li>
<li><p><a href="get-a-list-of-customers.md">顧客の一覧を取得する</a></p></li>
</ul>
<p>顧客の注文とサブスクリプションの管理</p>
<ul>
<li><p><a href="get-all-of-a-customer-s-orders.md">顧客&#39;の注文をすべて取得する</a></p></li>
<li><p><a href="get-a-list-of-orders-by-customer-and-billing-cycle-type.md">顧客と請求サイクルの種類別に注文の一覧を取得する</a></p></li>
<li><p><a href="get-a-collection-of-entitlements.md">エンタイトルメントのコレクションを取得する</a></p></li> 
<li><p><a href="get-all-of-a-customer-s-subscriptions.md">顧客&#39;のサブスクリプションを取得する</a></p></li>
<li><p><a href="update-the-nickname-for-a-subscription.md">サブスクリプションのニックネームを更新する</a></p></li>
</ul>
<p>顧客アカウントの詳細の管理</p>
<ul>
<li><p><a href="get-all-of-a-customer-s-billing-profiles.md">顧客&#39;の請求プロファイルを取得する</a></p></li>
<li><p><a href="update-a-customer-s-billing-profile.md">顧客&#39;の請求プロファイルを更新する</a></p></li>
<li><p><a href="get-a-customer-s-company-profile.md">顧客&#39;の会社プロファイルを取得する</a></p></li>
<li><p><a href="update-a-customer-s-usage-spending-budget.md">顧客&#39;の使用支出予算を更新する</a></p></li>
<li><p><a href="add-a-verified-domain-for-a-customer.md">顧客の確認済みドメインを追加する</a></p></li>
<li><p><a href="confirm-customer-consent.md">Microsoft Cloud 契約に関するお客様の同意を確認する</a></p></li>
<li><p><a href="get-agreement-metadata.md">Microsoft Cloud 契約の契約メタデータを取得する</a></p></li>
<li><p><a href="get-confirmation-of-customer-consent.md">Microsoft Cloud 契約に関するお客様の同意の確認を取得する</a></p></li>
<li><p><a href="get-a-partner-s-validation-codes.md">パートナーの確認コードを取得する</a></p></li>
<li><p><a href="get-a-customer-s-qualification.md">顧客の資格情報を取得する</a></p></li>
<li><p><a href="update-a-customer-s-qualification.md">顧客の資格情報を更新する</a></p></li>
</ul>
<p>ユーザーアカウントを管理し、ライセンスを割り当てる</p>
<ul>
<li><p><a href="get-a-user-account-by-id.md">ユーザー アカウントを ID で取得する</a></p></li>
<li><p><a href="create-user-accounts-for-a-customer.md">顧客のユーザー アカウントを作成する</a></p></li>
<li><p><a href="delete-user-accounts-for-a-customer.md">顧客のユーザー アカウントを削除する</a></p></li>
<li><p><a href="update-user-accounts-for-a-customer.md">顧客のユーザー アカウントを更新する</a></p></li>
<li><p><a href="view-a-deleted-user.md">顧客の削除されたユーザーを表示する</a></p></li>
<li><p><a href="restore-a-user-for-a-customer.md">顧客の削除されたユーザーを復元する</a></p></li>
<li><p><a href="get-a-list-of-all-user-accounts-for-a-customer.md">顧客のすべてのユーザー アカウントの一覧を取得する</a></p></li>
<li><p><a href="reset-user-password-for-a-customer.md">顧客のユーザー パスワードをリセットする</a></p></li>
<li><p><a href="get-user-roles-for-a-customer.md">顧客のユーザー ロールを取得する</a></p></li>
<li><p><a href="set-user-roles-for-a-customer.md">顧客のユーザー ロールを設定する</a></p></li>
<li><p><a href="remove-customer-user-from-a-role.md">顧客ユーザーをロールから削除する</a></p></li>
<li><p><a href="get-a-list-of-available-licenses.md">利用可能なライセンスの一覧を取得する</a></p></li>
<li><p><a href="assign-licenses-to-a-user.md">ユーザーにライセンスを割り当てる</a></p></li>
<li><p><a href="check-which-licenses-are-assigned-to-a-user.md">ユーザーに割り当てられたライセンスを取得する</a></p></li>
<li><p><a href="get-licenses-assigned-to-a-user-by-license-group.md">ユーザーに割り当てられたライセンスをライセンス グループ別に取得する</a></p></li>
<li><p><a href="get-a-list-of-available-licenses-by-license-group.md">利用可能なライセンスの一覧をライセンス グループ別に取得する</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-orders.md">注文を管理する</a></p></td>
<td><p>購入 Azure Reserved VM Instances</p>
<ul>
<li><p><a href="purchase-azure-reservations.md">Azure Reservations を購入する</a></p></li>
</ul>
<p>1回限りの購入を行う</p>
<ul>
<li><p><a href="make-a-one-time-purchase.md">1 回限りの購入を行う</a></p></li> 
</ul>
<p>カタログからオファーを取得する</p>
<ul>
<li><p><a href="get-a-list-of-offer-categories-by-country-and-locale.md">市場別のプラン カテゴリの一覧を取得する</a></p></li>
<li><p><a href="get-a-list-of-offers-for-a-market.md">市場別のプランの一覧を取得する</a></p></li>
<li><p><a href="get-an-offer-by-id.md">ID でプランを取得する</a></p></li>
<li><p><a href="get-addon-offers-by-offer-id.md">プラン ID のアドオンを取得する</a></p></li>
<li><p><a href="get-a-list-of-products.md">製品の一覧を取得する</a></p></li>
<li><p><a href="get-a-product-by-id.md">ID で製品を取得する</a></p></li>
<li><p><a href="get-a-list-of-skus-for-a-product.md">製品の Sku の一覧を取得する</a></p></li>
<li><p><a href="get-a-sku-by-id.md">SKU に使用できる機能の一覧を取得する</a></p></li>
<li><p><a href="get-an-availability-by-id.md">ID で可用性を取得する</a></p></li>
<li><p><a href="check-inventory.md">在庫を確認する</a></p></li>
</ul>
<p>注文の管理</p>
<ul>
<li><p><a href="cancel-an-order-from-the-integration-sandbox.md">統合サンドボックスから注文をキャンセルする</a></p></li>
<li><p><a href="checkout-a-cart.md">カートを精算する</a></p></li>
<li><p><a href="create-a-cart.md">カートを作成する</a></p></li>
<li><p><a href="create-a-cart-with-add-ons.md">アドオンを扱うカートを作成する</a></p></li>
<li><p><a href="create-an-order.md">注文を作成する</a></p></li>
<li><p><a href="create-an-order-for-a-customer-of-an-indirect-reseller.md">間接リセラーの顧客の注文を作成する</a></p></li>
<li><p><a href="get-activation-link-by-order-line-item.md">注文明細でアクティブ化リンクを取得する</a></p></li>
<li><p><a href="get-an-order-by-id.md">ID で注文を取得する</a></p></li>
<li><p><a href="purchase-an-add-on-to-a-subscription.md">サブスクリプションのアドオンを購入する</a></p></li>
<li><p><a href="purchase-catalog-items.md">カタログ項目を購入する</a></p></li>
<li><p><a href="update-a-cart.md">カートを更新する</a></p></li>
</ul>
<p>Azure 予約 VM インスタンスの購入のサブスクリプションを有効にする</p>
<ul>
<li><p><a href="register-a-subscription.md">サブスクリプションを登録する</a></p></li>
<li><p><a href="get-subscription-registration-status.md">サブスクリプションの登録状態を取得する</a></p></li>
</ul>
<p>試用版への変換</p>
<ul>
<li><p><a href="get-a-list-of-trial-conversion-offers.md">試用版の変換プランの一覧を取得する</a></p></li>
<li><p><a href="convert-a-trial-subscription-to-paid.md">試用版サブスクリプションを有料版に変換する</a></p></li>
</ul>
<p>サブスクリプションの詳細を取得する</p>
<ul>
<li><p><a href="get-a-subscription-by-id.md">ID でサブスクリプションを取得する</a></p></li>
<li><p><a href="get-a-list-of-subscriptions-by-order.md">注文別のサブスクリプションの一覧を取得する</a></p></li>
<li><p><a href="get-a-list-of-add-ons-for-a-subscription.md">サブスクリプションのアドオンの一覧を取得する</a></p></li>
<li><p><a href="get-subscription-provisioning-status.md">サブスクリプションのプロビジョニング状態を取得する</a></p></li>
</ul>
<p>サブスクリプションの管理</p>
<ul>
<li><p><a href="change-the-quantity-of-a-subscription.md">サブスクリプションの数量を変更する</a></p></li>
<li><p><a href="update-autorenew-for-an-azure-marketplace-subscription.md">商用マーケットプレース サブスクリプションの自動更新を更新する</a></p></li>
<li><p><a href="suspend-a-subscription.md">サブスクリプションの中断</a></p></li>
<li><p><a href="reactivate-a-suspended-a-subscription.md">中断したサブスクリプションを再アクティブ化する</a></p></li>
<li><p><a href="transition-a-subscription.md">サブスクリプションを移行する</a></p></li>
<li><p><a href="cancel-an-azure-marketplace-subscription.md">商用マーケットプレース サブスクリプションをキャンセルする</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="provide-support.md">サポートを提供する</a></p></td>
<td><p>顧客のサービスを管理する</p>
<ul>
<li><p><a href="get-the-managed-services-for-a-customer-by-id.md">ID を使って顧客の管理サービスを取得する</a></p></li>
</ul>
<p>サポート連絡先の管理</p>
<ul>
<li><p><a href="get-a-subscription-s-support-contact.md">サブスクリプション&#39;のサポート連絡先を取得する</a></p></li>
<li><p><a href="update-a-subscription-s-support-contact.md">サブスクリプション&#39;のサポート連絡先を更新する</a></p></li>
</ul>
<p>サービスリクエストの管理</p>
<ul>
<li><p><a href="create-a-service-request-.md">サービス リクエストを作成する</a></p></li>
<li><p><a href="get-service-request-support-topics--pending-.md">サービス リクエストのサポート トピックを取得する</a></p></li>
<li><p><a href="get-all-service-requests-for-a-customer.md">顧客のサービス リクエストをすべて取得する</a></p></li>
<li><p><a href="get-service-request-details-by-id.md">ID でサービス リクエストの詳細を取得する</a></p></li> 
<li><p><a href="update-a-service-request.md">サービス リクエストを更新する</a></p></li>
</ul></td>
</tr>
<tr>
  <td><p><a href="https://docs.microsoft.com/partner/develop/referrals">紹介</a></p></td>
  <td><p>紹介</p>
    <ul>
      <li><p><a href="https://docs.microsoft.com/partner/develop/create-a-referral">紹介を作成する</a></p></li> 
      <li><p><a href="https://docs.microsoft.com/partner/develop/get-a-list-of-referrals">紹介の一覧を取得する</a></p></li> 
      <li><p><a href="https://docs.microsoft.com/partner/develop/get-a-referral-by-id">紹介を ID ごとに取得する</a></p></li> 
      <li><p><a href="https://docs.microsoft.com/partner/develop/update-a-referral">紹介を更新する</a></p></li> 
    </ul>
  </td>
</tr>
<tr>
<td><p><a href="utilities.md">ユーティリティ</a></p></td>
<td><p>ユーティリティ</p>
<ul>
<li><p><a href="validate-an-address.md">アドレスを確認する</a></p></li>
<li><p><a href="get-market-specific-validation-data.md">市場別の住所書式規則を取得する</a></p></li>
<li><p><a href="verify-domain-availability.md">ドメインが使用できるかどうかを確認する</a></p></li>
<li><p><a href="delete-a-customer-account-from-the-integration-sandbox.md">統合サンドボックスから顧客アカウントを削除する</a></p></li>
<li><p><a href="get-a-record-of-partner-center-activity-by-user.md">パートナー センター アクティビティのレコードを取得する</a></p></li>
</ul></td>
</tr>
</tbody>
</table>

## <a name="background"></a>背景

### <a name="who-is-involved-in-the-order-process"></a>注文プロセスに参加しているユーザー

Microsoft、ディストリビューター、リセラー、およびお客様。 ディストリビューターとリセラーは、多くの場合、**パートナー**と呼ばれています。

Microsoft は、お客様に販売するリセラーと直接連携することがあります。 また、Microsoft では、ディストリビューターとも連携しています。また、これらのディストリビューターは、お客様に販売するリセラーの独自のセットまたはチャネルで動作します。

### <a name="whats-getting-sold"></a>販売されるのはどのようなものですか?

Microsoft では、**プラン**の一覧を提供しています。 これらは、Office 365 や Intune などの製品の特定の Sku です。 プランは、**ライセンスベース**(コストはインストールされるコンピューターの数によって異なります) または**使用量ベース**(コストは、使用されるメモリと計算の量によって異なります) です。 詳細については、「[クラウドソリューションプロバイダープログラムのパートナーオファー](https://docs.microsoft.com/partner-center/csp-offers)」を参照してください。

CSP パートナーは、顧客を持つ再販業者であり、現在のプランリストから Microsoft 製品を販売します。 お客様が契約に署名した後、リセラーは1つ以上のプランを**注文**します。 一部のプランには、より多くの領域や追加機能など、親プランと共に追跡される**アドオン**が含まれています。 注文が処理された後、顧客が**サブスクリプション**を使用できるようになります。 Microsoft は、各顧客のライセンス数と使用量に基づいて、1か月ごとに販売店または再販業者に請求します。

サブスクリプションを追加したり、接続クライアント数やアドオンの数を増減させたりすることができます。 お客様が支払いに失敗した場合、サブスクリプションを誤って使用した場合、または不正行為に関与している場合は、Microsoft、ディストリビューター、または再販業者がすべてのサブスクリプションを中断できます。 CSP プログラムの制限内で再アクティブ化されていない場合は、永続的になります。

顧客が**使用できるサブスクリプションを確認**できます (ie は、現在有料で、中断されておらず、新しい順序で置き換えられていない)。
