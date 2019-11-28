---
title: Microsoft National Cloud のパートナーセンターのアプリの詳細を登録する
description: 開発者は、Azure portal を通じて Azure AD でアプリの詳細を登録する必要があります。 これにより、指定されたアプリのみがパートナーおよび顧客データに接続できるようになります。
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.assetid: 73C5926A-0DEB-42E5-8982-7E44A2031F0B
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 494c803af64d8affd126a8de05fcdb18d648d774
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489552"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud"></a>Microsoft National Cloud のパートナーセンターのアプリの詳細を登録する

適用対象:

- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

開発者は、Azure portal を通じて Azure AD でアプリの詳細を登録する必要があります。 これにより、指定されたアプリのみがパートナーおよび顧客データに接続できるようになります。

米国政府の Microsoft Cloud のパートナーセンターでは、現在、PowerShell を使用してアプリを管理する必要があります。 詳細については、 [Azure PowerShell リファレンスドキュメント](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0#applications)を参照してください。

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

米国政府機関向け Microsoft Cloud のパートナーセンター向けのアプリを作成する場合は、次の追加要件に注意してください。 Microsoft Cloud ドイツまたはパートナーセンターを対象としています。

## <a name="web-apps"></a>Web apps

Web アプリの場合は、次の手順を使用してアプリケーション ID を登録します。

### <a name="create-or-update-web-app"></a>Web アプリの作成または更新

1. [Azure portal アプリの登録](https://go.microsoft.com/fwlink/?linkid=2083908)ページに移動して、アプリを登録します。 職場または学校のアカウントまたは個人の Microsoft アカウントを使用して Azure portal にサインインします。

2. **[新規登録]** を選択します。 詳細については、「[クイックスタート: Microsoft identity platform](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app)へのアプリケーションの登録」を参照してください。

### <a name="configure-api-access-permissions-for-web-app"></a>Web アプリの API アクセス許可を構成する

1. アプリを選択します。 Web アプリの **[設定]** にアクセスします。
2. **[API アクセス]** セクションで、 **[必要なアクセス許可]** を選択します。
3. Windows Azure Active directory のアクセス許可の場合:
    1. **Windows Azure Active Directory のアクセス許可**を選択します。
    2. **アプリケーションのアクセス許可** で、ディレクトリデータの読み取り を選択します。
    3. アクセス許可を保存します。
4. Web アプリの **[プロパティ]** セクションで、アプリケーション ID をメモしておきます。

### <a name="add-a-secret-key-to-your-app"></a>アプリへの秘密鍵の追加

1. Web アプリの **[キー]** セクションにアクセスします。
2. キーの説明を入力し、必要に応じて [期間] を1または2年として選択します。
3. 秘密キーの値を保存してコピーします。 **このページから移動すると、この値は再び表示されません。**

Web アプリの構成の詳細は次のとおりです。

- アプリケーション ID
- アプリケーションシークレット

### <a name="register-the-web-app-in-partner-center"></a>パートナーセンターで Web アプリを登録する

1. <https://partnercenter.microsoft.com>にログインします。
2. **[ダッシュボード]** を選択し、 **[アカウントの設定]** 、 **[アプリの管理]** の順に選択します。
3. **[Web アプリ]** セクションで、 **[既存のアプリの登録]** を選択します。
4. Microsoft Azure 管理ポータルで作成した web アプリを選択します。
5. **[アプリの登録]** を選択します。

## <a name="native-apps"></a>ネイティブアプリ

ネイティブアプリをパートナーセンターに登録する必要はありません。 ただし、これらのアプリは、パートナーセンター Api へのアクセスを提供するように構成する必要があります。

>[!NOTE]
>Microsoft Azure 管理ポータルでネイティブアプリを作成する前に、パートナーテナントの管理者ユーザー資格情報を使用してパートナーセンターにログインします。 これにより、アプリのアクセス許可を有効にするための設定がテナントに作成されます。

### <a name="create-native-app"></a>ネイティブアプリの作成

1. [Azure portal アプリの登録](https://go.microsoft.com/fwlink/?linkid=2083908)ページに移動して、アプリを登録します。 職場または学校のアカウントまたは個人の Microsoft アカウントを使用して Azure portal にサインインします。

2. **[新規登録]** を選択します。 詳細については、「[クイックスタート: Microsoft identity platform](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app)へのアプリケーションの登録」を参照してください。

### <a name="configure-api-access-permissions-for-native-app"></a>ネイティブアプリの API アクセス許可を構成する

1. アプリを選択します。 **[設定]** にアクセスします。
2. API アクセス で、**必要なアクセス許可** を選択します。
3. **Windows Azure Active Directory のアクセス許可**を選択します。 [委任された**アクセス許可**] で、次のアクセス許可を選択します。
    - **サインインとユーザープロファイルの読み取り**
    - **ディレクトリデータの読み取り**
    - **サインインしているユーザーとしてディレクトリにアクセスする**
    - **すべてのグループの読み取り**
4. アクセス許可を保存します。
5. **[必要なアクセス許可]** で **[追加]** を選択します。
6. [ **API の選択]** を選択します。
    1. 検索ボックスに「 **Microsoft パートナーセンター** 」と入力し、結果の一覧から選択します。
    2. **[選択]** を選択します。
7. **[アクセス許可の選択**] を選択します。
    1. **[アクセスパートナーセンターの PPE]** を選択します。
    2. **[選択]** を選択します。
8. **[完了]** を選択します。

>[!IMPORTANT]
> アプリのプロパティのアプリケーション ID をメモしておきます。

ネイティブアプリをパートナーセンターに登録する必要はありませんが、ネイティブアプリは admin 同意である必要があります。 ネイティブアプリのアプリケーション ID をメモしておきます。