---
title: 開始
description: Partner Center SDK には、パートナーが顧客、サブスクリプション、注文データを管理するために使用できるマネージド API と REST API が含まれています。
ms.assetid: D9A91032-CA5B-4CD2-ADBA-6C5513E05D32
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 49b08fbb6896a484aaf61563a08802bafbe9a541
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157244"
---
# <a name="get-started"></a>開始

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Partner Center SDK には、パートナーが顧客、サブスクリプション、注文データを管理するために使用できるマネージド API と REST API が含まれています。

## <a name="get-the-code"></a>コードを入手する

[Partner Center SDK のダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> 間接リセラーのパートナー センターへの API アクセスは、サポートされているシナリオではありません。

## <a name="determine-your-version-of-partner-center"></a>パートナー センターのバージョンを確認する

一部のバージョンのパートナー センターでは、SDK 全体を使用できません。 詳細については、「[Microsoft National クラウドのパートナーセンター向けの開発](developing-for-partner-center-for-microsoft-national-cloud.md)」を参照してください。

## <a name="get-the-samples"></a>サンプルの入手

C# スニペット、REST サンプル、サンプル アプリの詳細については、「[パートナー センターのサンプル](partner-center-samples.md)」を参照してください。

## <a name="test-vs-production"></a>テストと運用

最初のうちは、コードを書いてテストするときに、統合サンドボックス アカウント (および対応するトークン) を使用して、会社のコストとなる新しい料金が誤って生じないようにする必要があります。 このテスト環境の詳細については、「[パートナーセンターでの API アクセスの設定](set-up-api-access-in-partner-center.md)」を参照してください。

ソリューションをテストして実際の顧客アカウントで使用する準備ができたら、プライマリ パートナー センター アカウントに対応する Azure AD クライアント アプリとシークレットを使用するようにトークンを更新する必要があります。

運用環境でのテスト (TiP) や統合サンドボックスの詳細など、テストとデバッグのヒントと提案については、「[テストとデバッグ](test-and-debug.md)」を参照してください。

## <a name="configure-your-authentication"></a>認証を構成する

Partner Center API を使用できるように Azure AD 認証を構成するには、「[パートナー センターの認証](partner-center-authentication.md)」を参照してください。

> [!IMPORTANT]
> Microsoft では、Microsoft Azure 多要素認証 (MFA) アーキテクチャを介してクラウド ソリューション プロバイダー (CSP) パートナーとコントロール パネル ベンダー (CPV) を認証することができる、セキュリティで保護されたスケーラブルなフレームワークを導入しています。
パートナー センターでは認証に Azure AD を使用するため、Partner Center API を使用するには、認証設定を正しく構成する必要があります。
>
> 詳細については、「[セキュリティで保護されたアプリケーション モデルを有効にする](enable-secure-app-model.md)」を参照してください。

## <a name="get-help"></a>ヘルプを取得する

パートナーは、[Partner Center SDK Yammer グループ](https://go.microsoft.com/fwlink/p/?LinkID=717360)でサポートを受けることができます。 よりパーソナル設定されたヘルプを表示するために、開発者は MPN サポートの特典や Premier サポートを使用できます。

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a>パートナー センターAPI および SDK 早期導入者プログラムにご参加ください。

Microsoft と協力してパートナー機能を開発する方法については、「[Partner Center API および SDK 早期導入者プログラムにご参加ください](early-adopter-program.md)」を参照してください。
