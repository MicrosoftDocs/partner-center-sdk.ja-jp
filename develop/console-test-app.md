---
title: コンソールテストアプリ
description: このコンソールテストアプリは、パートナーセンター Api でサポートされているすべてのシナリオのサンプルコードを提供します。 テストにも使用できます。
ms.assetid: 56F5B4C6-CE87-4D13-9D8C-09F38E946292
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 35ebb92e8e9705cbce8c629d0a862613cc2f50b6
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412847"
---
# <a name="console-test-app"></a>コンソールテストアプリ

適用対象

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

コンソールテストアプリはと Java でC#提供され、パートナーセンター api でサポートされているすべてのシナリオのサンプルコードを提供します。 テストにも使用できます。

## <a name="get-the-code"></a>コードを入手する

コンソールテストアプリのサンプルコードをダウンロードします。

## <a name="net"></a>.NET

[サンプルコードをダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=746682)し、必要に応じて変更します。

> [!IMPORTANT]
> アプリケーションをビルドする前に、 *app.config*ファイルの値を更新して、[パートナーセンターの認証](partner-center-authentication.md)で作成した Azure AD 認証情報を反映させます。 具体的には、開発の初期段階で、または実稼働環境でのテストの際に、統合サンドボックスアカウントの設定を使用する必要があります。

*App.config*ファイルの**ScenarioSettings**では、実行するシナリオに自動的に渡されるパラメーターを設定できます。

実行されるシナリオの一覧を変更するには、 **Ipartnerscenario\[\] Mainscenarios**をコメントアウトするか、 *Program.cs*ファイルに記載されている個々の**シナリオの取得**メソッドをコメントアウトします。

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

[サンプルコードをダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=2026887)し、必要に応じて変更します。

> [!IMPORTANT]
> アプリケーションをビルドする前に、 *SamplesConfigurations*ファイルの値を更新して、[パートナーセンターの認証](partner-center-authentication.md)で作成した Azure AD 認証情報を反映させます。 具体的には、開発の初期段階で、または実稼働環境でのテストの際に、統合サンドボックスアカウントの設定を使用する必要があります。

*SamplesConfiguration*ファイルの**ScenarioSettings**では、実行するシナリオに自動的に渡されるパラメーターを設定できます。

実行されるシナリオの一覧を変更するには、 **Ipartnerscenario\[\] Mainscenarios**にコメントアウトするか、または*java*ファイルに含まれる個々の**Get** scenario メソッドにコメントアウトします。

## <a name="what-to-change"></a>変更する内容

次の一覧を使用して、サンプルコードで変更または変更しない内容を決定します。

### <a name="partnerservicesettings"></a>PartnerServiceSettings

**Partnerservicesettings**の場合は、次のように変更しないでください。

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

これらの設定はすべて、サンプルの API 呼び出しが適切に機能するために必要です。

### <a name="userauthentication"></a>UserAuthentication

**Userauthentication**の場合は、次のように変更する必要があります。

- **ApplicationId** (ログインに使用される AZURE ACTIVE DIRECTORY アプリケーション ID)
- **ユーザー名**(active directory ユーザー名)
- **パスワード**(active directory のパスワード)。

変更しない:

- **ResourceUrl**
- **RedirectUrl**

### <a name="appauthentication"></a>Microsoft.azure.services.appauthentication

**Appauthentication**の場合は、次のように変更する必要があります。

- **ApplicationId** (アプリケーションログインに使用する active DIRECTORY アプリケーション ID)
- **Applicationsecret** (アプリケーションログインに使用する active directory アプリケーションシークレット)
- **ドメイン**(アプリケーションがホストされている active directory ドメイン)

### <a name="scenariosettings"></a>ScenarioSettings

**ScenarioSettings**の場合は、次のように変更しないでください。

- 顧客**domainsuffix** (新しい顧客を作成するときに使用されるドメインサフィックス)

オプションの設定。 空白のままにしておくと、必要に応じてシナリオを実行するときに、この情報を入力する必要があります。

- **CustomerIdToDelete** (削除に使用された顧客の ID)
- **Defaultcustomerid** (顧客関連のシナリオで使用する顧客 ID)
- **DefaultInvoiceID** (請求書のシナリオで使用する請求書 ID)
- **Partnermpnid** (間接パートナーシナリオで使用する PARTNER MPN ID)
- **DefaultServiceRequestId** (サービス要求シナリオで使用するサービス要求 ID)
- **Defaultsupporttopic id** (サービス要求シナリオで使用するサポートトピック id)
- **Defaultofferid** (プランのシナリオで使用するオファー ID)
- **Defaultorderid** (順序のシナリオで使用する注文 ID)
- **Defaultsubscriptionid** (サブスクリプションのシナリオで使用するサブスクリプション ID)

変更する場合は省略可能。 これらの設定はすべて、ページングされたコンテンツを取得するときのページごとのエントリの量を指定します。

- **顧客 Pagesize**
- **InvoicePageSize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**