---
title: Microsoft National Cloud のパートナーセンターのアプリの詳細を登録する
description: 開発者は、Azure portal を通じて Azure AD でアプリの詳細を登録する必要があります。 これにより、指定されたアプリのみがパートナーおよび顧客データに接続できるようになります。
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: acb84caddfc42de957b4e45b781f650ec9640038
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094420"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud"></a>Microsoft National Cloud のパートナーセンターのアプリの詳細を登録する

**適用対象:**

- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

開発者は、Azure portal を通じて Azure AD でアプリの詳細を登録する必要があります。 これにより、指定されたアプリのみがパートナーおよび顧客データに接続できるようになります。

米国政府の Microsoft Cloud のパートナーセンターでは、現在、PowerShell を使用してアプリを管理する必要があります。 詳細については、 [Azure PowerShell リファレンスドキュメント](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0#applications)を参照してください。

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

米国政府機関向け Microsoft Cloud のパートナーセンター向けのアプリを作成する場合は、次の追加要件に注意してください。 Microsoft Cloud ドイツまたはパートナーセンターを対象としています。

## <a name="web-apps"></a>Web アプリ

Web アプリの場合は、次の手順を使用してアプリケーション ID を登録します。

### <a name="create-or-update-web-app"></a>Web アプリの作成または更新

1. [Azure portal アプリの登録](https://go.microsoft.com/fwlink/?linkid=2083908)ページに移動して、アプリを登録します。 職場または学校のアカウントまたは個人の Microsoft アカウントを使用して Azure portal にサインインします。

2. **[新規登録]** を選択します。 詳細については、「[クイック スタート: Microsoft ID プラットフォームにアプリケーションを登録する](https://docs.microsoft.com/azure/active-directory/develop/quickstart-register-app)」を参照してください。

### <a name="configure-api-access-permissions-for-web-app"></a>Web アプリの API アクセス許可を構成する

1. アプリを選びます。 Web アプリの [**設定**] にアクセスします。

2. [ **API アクセス**] セクションで、[**必要なアクセス許可**] を選択します。

3. Windows Azure Active directory のアクセス許可の場合:

    1. **Windows Azure Active Directory のアクセス許可**を選択します。

    2. [**アプリケーションのアクセス許可**] で、[ディレクトリデータの読み取り] を選択します。

    3. アクセス許可を保存します。

4. Web アプリの [**プロパティ**] セクションで、アプリケーション ID をメモしておきます。

### <a name="add-a-secret-key-to-your-app"></a>アプリへの秘密鍵の追加

1. Web アプリの [**キー** ] セクションにアクセスします。

2. キーの説明を入力し、必要に応じて [期間] を1または2年として選択します。

3. 秘密キーの値を保存してコピーします。 **このページから移動すると、この値は再び表示されません。**

Web アプリの構成の詳細は次のとおりです。

- アプリケーション ID
- アプリケーション シークレット

### <a name="register-the-web-app-in-partner-center"></a>パートナーセンターで Web アプリを登録する

1. にログイン [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) します。

2. [**ダッシュボード**] を選択し、[**アカウントの設定**]、[**アプリの管理**] の順に選択します。

3. [ **Web アプリ**] セクションで、[**既存のアプリの登録**] を選択します。

4. Azure portal で作成した web アプリを選択します。

5. [**アプリの登録**] を選択します。

## <a name="native-apps"></a>ネイティブ アプリ

ネイティブアプリをパートナーセンターに登録する必要はありません。 ただし、これらのアプリは、パートナーセンター Api へのアクセスを提供するように構成する必要があります。

>[!NOTE]
>Azure portal でネイティブアプリを作成する前に、パートナーテナントの管理者ユーザー資格情報を使用してパートナーセンターにログインします。 これにより、アプリのアクセス許可を有効にするための設定がテナントに作成されます。

### <a name="create-native-app"></a>ネイティブ アプリを作成する

1. [Azure portal アプリの登録](https://go.microsoft.com/fwlink/?linkid=2083908)ページに移動して、アプリを登録します。 職場または学校のアカウントまたは個人の Microsoft アカウントを使用して Azure portal にサインインします。

2. **[新規登録]** を選択します。 詳細については、「[クイック スタート: Microsoft ID プラットフォームにアプリケーションを登録する](https://docs.microsoft.com/azure/active-directory/develop/quickstart-register-app)」を参照してください。

### <a name="configure-api-access-permissions-for-native-app"></a>ネイティブアプリの API アクセス許可を構成する

1. アプリを選びます。 **[設定]** に移動します。

2. [API アクセス] で、[**必要なアクセス許可**] を選択します。

3. **Windows Azure Active Directory のアクセス許可**を選択します。 [委任された**アクセス許可**] で、次のアクセス許可を選択します。

    - **サインインとユーザー プロファイルの読み取り**
    - **ディレクトリ データの読み取り**
    - **サインインしたユーザーとしてディレクトリにアクセスする**
    - **すべてのグループの読み取り**

4. アクセス許可を保存します。

5. [**必要なアクセス許可**] で [**追加**] を選択します。

6. **[API を選択する]** を選択します。

    1. 検索ボックスに「 **Microsoft パートナーセンター** 」と入力し、結果の一覧から選択します。

    2. **[選択]** を選択します。

7. **[アクセス許可の選択]** を選択します。

    1. [**アクセスパートナーセンターの PPE**] を選択します。
    
    2. **[選択]** を選択します。

8. [**完了**] を選択します。

>[!IMPORTANT]
> アプリのプロパティのアプリケーション ID をメモしておきます。

ネイティブアプリをパートナーセンターに登録する必要はありませんが、ネイティブアプリは admin 同意である必要があります。 ネイティブアプリのアプリケーション ID をメモしておきます。
