---
title: 開始
description: Partner Center SDK には、パートナーが顧客、サブスクリプション、注文データを管理するために使用できるマネージド API と REST API が含まれています。
ms.assetid: D9A91032-CA5B-4CD2-ADBA-6C5513E05D32
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3d47c3c41a7f6a23d8be6e9c20c16e6f7c01f275
ms.sourcegitcommit: 98ec47d226a0b56f329e55ba881e476e2afff971
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "74995227"
---
# <a name="get-started"></a>開始

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Partner Center SDK には、パートナーが顧客、サブスクリプション、注文データを管理するために使用できるマネージド API と REST API が含まれています。

## <a name="span-idget_the_codespan-idget_the_codespan-idget_the_codeget-the-code"></a><span id="Get_the_code"/><span id="get_the_code"/><span id="GET_THE_CODE"/>コードを入手する

[Partner Center SDK のダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=746681)  

> [!NOTE]  
> 間接リセラーのパートナー センターへの API アクセスは、サポートされているシナリオではありません。

## <a name="span-iddetermine_your_version_of_partner_centerspan-iddetermine_your_version_of_partner_centerspan-iddetermine_your_version_of_partner_centerdetermine-your-version-of-partner-center"></a><span id="Determine_your_version_of_Partner_Center"/><span id="determine_your_version_of_partner_center"/><span id="DETERMINE_YOUR_VERSION_OF_PARTNER_CENTER"/>パートナー センターのバージョンを確認する

一部のバージョンのパートナー センターでは、SDK 全体を使用できません。 詳細については、「[Microsoft National クラウドのパートナーセンター向けの開発](developing-for-partner-center-for-microsoft-national-cloud.md)」を参照してください。

## <a name="span-idget_the_samplesspan-idget_the_samplesspan-idget_the_samplesget-the-samples"></a><span id="Get_the_samples"/><span id="get_the_samples"/><span id="GET_THE_SAMPLES"/>サンプルの入手

C# スニペット、REST サンプル、サンプル アプリの詳細については、「[パートナー センターのサンプル](partner-center-samples.md)」を参照してください。

## <a name="span-idsdk_test_vs_prodspan-idsdk_test_vs_prodtest-vs-production"></a><span id="sdk_test_vs_prod"/><span id="SDK_TEST_VS_PROD"/>テストと運用

最初のうちは、コードを書いてテストするときに、統合サンドボックス アカウント (および対応するトークン) を使用して、会社のコストとなる新しい料金が誤って生じないようにする必要があります。 このテスト環境の詳細については、「[パートナーセンターでの API アクセスの設定](set-up-api-access-in-partner-center.md)」を参照してください。

ソリューションをテストして実際の顧客アカウントで使用する準備ができたら、プライマリ パートナー センター アカウントに対応する Azure AD クライアント アプリとシークレットを使用するようにトークンを更新する必要があります。

運用環境でのテスト (TiP) や統合サンドボックスの詳細など、テストとデバッグのヒントと提案については、「[テストとデバッグ](test-and-debug.md)」を参照してください。

## <a name="span-idsdk_config_authspan-idsdk_config_authconfigure-your-authentication"></a><span id="sdk_config_auth"/><span id="SDK_CONFIG_AUTH"/>認証を構成する

Partner Center API を使用できるように Azure AD 認証を構成するには、「[パートナー センターの認証](partner-center-authentication.md)」を参照してください。  

> [!IMPORTANT]
> Microsoft では、Microsoft Azure 多要素認証 (MFA) アーキテクチャを介してクラウド ソリューション プロバイダー (CSP) パートナーとコントロール パネル ベンダー (CPV) を認証することができる、セキュリティで保護されたスケーラブルなフレームワークを導入しています。
パートナー センターでは認証に Azure AD を使用するため、Partner Center API を使用するには、認証設定を正しく構成する必要があります。 
> 
> 詳細については、「[セキュリティで保護されたアプリケーション モデルを有効にする](enable-secure-app-model.md)」を参照してください。

## <a name="span-idget_helpspan-idget_helpspan-idget_helpget-help"></a><span id="Get_help"/><span id="get_help"/><span id="GET_HELP"/>サポートを受ける

パートナーは、[Partner Center SDK Yammer グループ](https://go.microsoft.com/fwlink/p/?LinkID=717360)でサポートを受けることができます。 よりパーソナル設定されたヘルプを表示するために、開発者は MPN サポートの特典や Premier サポートを使用できます。

## <a name="span-idearly_adopter_programspan-idearly_adopter_programspan-idearly_adopter_programjoin-the-partner-center-api-and-sdk-early-adopter-program"></a><span id="Early_adopter_program"/><span id="early_adopter_program"/><span id="EARLY_ADOPTER_PROGRAM"/>Partner Center API および SDK 早期導入者プログラムにご参加ください

Microsoft と協力してパートナー機能を開発する方法については、「[Partner Center API および SDK 早期導入者プログラムにご参加ください](early-adopter-program.md)」を参照してください。