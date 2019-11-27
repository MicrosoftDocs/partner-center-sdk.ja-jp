---
title: はじめに
description: パートナーセンター SDK には、顧客、サブスクリプション、および注文データを管理するために使用する、管理された API と REST API が含まれています。
ms.assetid: D9A91032-CA5B-4CD2-ADBA-6C5513E05D32
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 945b8df7d26f8d14386870979f69e3fdbe18d04f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487282"
---
# <a name="get-started"></a>はじめに

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーセンター SDK には、顧客、サブスクリプション、および注文データを管理するために使用する、管理された API と REST API が含まれています。

## <a name="span-idget_the_codespan-idget_the_codespan-idget_the_codeget-the-code"></a>コードの取得 <span id="GET_THE_CODE"/><span id="get_the_code"/>の <span id="Get_the_code"/>

[パートナーセンター SDK をダウンロードする](http://go.microsoft.com/fwlink/p/?LinkId=746681)  

> [!NOTE]  
> 間接リセラーのパートナーセンターへの API アクセスは、サポートされているシナリオではありません。

## <a name="span-iddetermine_your_version_of_partner_centerspan-iddetermine_your_version_of_partner_centerspan-iddetermine_your_version_of_partner_centerdetermine-your-version-of-partner-center"></a><span id="Determine_your_version_of_Partner_Center"/><span id="determine_your_version_of_partner_center"/><span id="DETERMINE_YOUR_VERSION_OF_PARTNER_CENTER"/>パートナーセンターのバージョンを確認する

一部のバージョンのパートナーセンターでは、SDK 全体を利用できません。 詳細については、「 [Microsoft National Cloud のパートナーセンター向けの開発](developing-for-partner-center-for-microsoft-national-cloud.md)」を参照してください。

## <a name="span-idget_the_samplesspan-idget_the_samplesspan-idget_the_samplesget-the-samples"></a>サンプルを取得 <span id="GET_THE_SAMPLES"/><span id="get_the_samples"/>の <span id="Get_the_samples"/>

C#スニペット、REST サンプル、サンプルアプリの詳細については、「[パートナーセンターのサンプル](partner-center-samples.md)」を参照してください。

## <a name="span-idsdk_test_vs_prodspan-idsdk_test_vs_prodtest-vs-production"></a><span id="sdk_test_vs_prod"/><span id="SDK_TEST_VS_PROD"/>テストと実稼働

コードを記述してテストしている間は、統合サンドボックスアカウント (および対応するトークン) を使用して、会社が支払いを行う新しい料金が誤って発生するのを避ける必要があります。 このテスト環境の詳細については、「[パートナーセンターでの API アクセスの設定](set-up-api-access-in-partner-center.md)」を参照してください。

ソリューションをテストし、実際の顧客アカウントで使用する準備ができたら、プライマリパートナーセンターアカウントに対応する Azure AD クライアントアプリとシークレットを使用するように、トークンを更新する必要があります。

実稼働 (TiP) テストと統合サンドボックスの詳細など、テストとデバッグに関するヒントと提案については、「[テストおよびデバッグ](test-and-debug.md)」を参照してください。

## <a name="span-idsdk_config_authspan-idsdk_config_authconfigure-your-authentication"></a>認証 <span id="SDK_CONFIG_AUTH"/>構成 <span id="sdk_config_auth"/>

パートナーセンター Api を使用できるように Azure AD 認証を構成するには、「[パートナーセンターの認証](partner-center-authentication.md)」を参照してください。  

> [!IMPORTANT]
> Microsoft では、Microsoft Azure multi-factor authentication (MFA) アーキテクチャを使用して、クラウドソリューションプロバイダー (CSP) パートナーとコントロールパネルベンダー (CPV) を認証するための、セキュリティで保護されたスケーラブルなフレームワークを導入しています。
パートナーセンターは認証に Azure AD を使用し、パートナーセンター Api を使用するには、認証設定を正しく構成する必要があります。 
> 
> 詳細については、「[セキュリティ保護されたアプリケーションモデルの有効化](enable-secure-app-model.md)」を参照してください。

## <a name="span-idget_helpspan-idget_helpspan-idget_helpget-help"></a><span id="get_help"/>の <span id="Get_help"/><span id="GET_HELP"/>ヘルプの表示

パートナーは、[パートナーセンター SDK Yammer グループ](http://go.microsoft.com/fwlink/p/?LinkID=717360)でサポートを受けることができます。 パーソナライズされたヘルプを表示するために、開発者は MPN サポートの特典や Premier サポートを使用できます。

## <a name="span-idearly_adopter_programspan-idearly_adopter_programspan-idearly_adopter_programjoin-the-partner-center-api-and-sdk-early-adopter-program"></a>パートナーセンター API および SDK 早期導入プログラムに参加 <span id="EARLY_ADOPTER_PROGRAM"/><span id="early_adopter_program"/><span id="Early_adopter_program"/>

パートナーの機能の開発において Microsoft と協力する方法については、「[パートナーセンター API と SDK 早期導入プログラムに参加](early-adopter-program.md)する」を参照してください。