---
title: CSP カスタマー web ネットショップ
description: このサンプル web サイトコードは、お客様が Microsoft 製品へのサブスクリプションを購入するための作業オンラインストアを示しています。
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
# <a name="csp-customer-web-storefront"></a>CSP カスタマー web ネットショップ

適用対象:

- パートナー センター

> [!NOTE]
> このサンプルアプリは、パートナーセンターのグローバルインスタンスにのみ適用されます。 Microsoft Cloud ドイツのパートナーセンターや米国政府機関向けのパートナー Microsoft Cloud センターには適用されません。

[パートナーセンターの店舗](https://github.com/Microsoft/Partner-Center-Storefront)は、お客様が Microsoft 製品のサブスクリプションを購入するために使用できるオンラインストアの**サンプル web サイト**です。 独自の**サンプルコード**を変更して、オファーの[構成](#configure-offers)、ブランドの[追加](#configure-branding)、[支払い方法の追加](#configure-payment-types)を行うことができます。

## <a name="sample-code"></a>サンプル コード

GitHub から[パートナーセンターのサンプルコード](https://github.com/Microsoft/Partner-Center-Storefront)をダウンロードします。

## <a name="configure-authentication"></a>認証設定の構成

アプリケーションをビルドする前に、web.config ファイルの次の値を更新して、[パートナーセンターの認証](partner-center-authentication.md)で作成した Azure AD 認証情報を反映させます。 統合サンドボックスアカウントの設定は、初期開発時または運用環境でのテスト (TiP) で使用する必要があります。

- **partnerCenter. applicationId**
- **partnerCenter. applicationSecret**
- **partnerCenter. ドメイン**
- **webPortal. clientId**
- **webPortal. clientSecret**
- **webPortal. ドメイン**
- **webPortal. azureStorageConnectionString**

## <a name="configure-offers"></a>オファーの構成

**OfferCatalogViewModel**のプランセット (**MicrosoftOffer**) を構成できます。

## <a name="configure-branding"></a>ブランドの構成

このサンプル web サイトでは、 *BrandingConfiguration.cs*と*PortalBranding.cs*の次の会社とブランドの情報を追跡します。

- 組織名
- 組織のロゴ
- ヘッダーイメージ
- プライバシーに関する契約
- 連絡先の電子メール
- 連絡先の電話番号
- サポート電子メール
- サポートの電話番号

### <a name="configure-payment-types"></a>支払いの種類を構成する

アプリは現在、 *PayPalGateway.cs*で実装されている PayPal ゲートウェイを使用しています。