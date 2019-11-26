---
title: Set up API access in Partner Center
description: Set up accounts for developing against the Partner Center SDK and test in the integration sandbox.
ms.assetid: 182A6831-6F00-4762-9A86-327BF87EA6AC
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 55c7259943dae2cd34ead9583f95afc38df47a3f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488062"
---
# <a name="set-up-api-access-in-partner-center"></a>Set up API access in Partner Center

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター
- Microsoft Cloud ドイツのパートナー センター

This topic describes the accounts you need to develop against the Partner Center SDK. This topic also explains how to create an [integration sandbox account](#integration-sandbox-account) and test in the integration sandbox.

## <a name="account-definitions"></a>Account definitions

API の統合とテストに役立つように、パートナー センターは次の 2 種類のアカウントをサポートします。

### <a name="primary-partner-account"></a>Primary Partner account

This account is where you create real orders for real customers. If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Dashboard UI, they will be treated as official orders for real customers. これらは請求書に反映され、貴社はその料金を支払うものとします。

### <a name="integration-sandbox-account"></a>統合サンドボックス アカウント

This account is for testing your code and its integration with the Partner Center APIs before you deploy it broadly. 統合サンドボックス アカウントにサインイン中に行う変更とトランザクションは、請求書には表示されません。

統合サンドボックス アカウントとプライマリ アカウントは独立して機能し、管理者アカウント、ユーザー アカウント、顧客、注文、サブスクリプションなどのデータは共有されません。

統合サンドボックスでは、限られた数の顧客、注文、サブスクリプション、シートなどのトランザクションがサポートされます。

ポリシーでは、統合サンドボックス アカウントは統合テストのみを目的としています。

By default, there is no integration sandbox account. You must create one yourself if you plan to use the Partner Center SDK.

## <a name="set-up-your-accounts"></a>Set up your accounts

This section describes how to set up a primary Partner account and an integration sandbox account for the Partner Center SDK.

### <a name="create-an-integration-sandbox"></a>統合サンドボックスを作成する

1. Sign in to Partner Dashboard with a global admin account (your primary Partner account.)
2. From the **Settings** menu (gear icon), choose **Partner settings**.
3. On the **Account settings** page, choose **Integration sandbox**.

    >[!NOTE]
    >If you don't see an Integration sandbox option, you might not have a global admin account. You also might be using an integration sandbox account and an integration sandbox has already been set up.

4. Enter the contact information for the integration sandbox admin account. Then, choose **Create account**. Wait a few minutes for a confirmation message that the account has been created.
5. After you see the confirmation message, sign out of Partner Dashboard.
6. Sign back in with your new integration sandbox admin account. Be sure to use the format **username@domain** for your credentials along with the password that you just specified.
7. Choose **Set Up Account** above **Current Tasks** to complete the sandbox account setup.

### <a name="enable-api-access"></a>API アクセスを有効にする

After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox. You need to enable access to the API separately for both your primary Partner account and your integration sandbox account.

1. Sign into Partner Dashboard using a global admin account.
2. From the **Settings** menu (gear icon), select **Partner settings**.
3. On the **Account settings** page, choose **App management**.
4. If you do not already have an existing app, add a new web app. If you have an existing web app, choose the **Add key** button.
5. Copy the app registration information, especially the **Key** if you're creating a web app, and store it in a safe place.
6. Sign out of Partner Dashboard.
7. Sign back in with your integration sandbox account. Repeat steps 2-5 to enable API access in the integration sandbox.

## <a name="write-and-test-code"></a>Write and test code

You can write code and test code in the integration sandbox. You'll need the following information to [set up Partner Center authentication](partner-center-authentication.md) with Azure AD.

| Item name | Item location |
| --------- | ------------- |
| アプリ ID /クライアント ID | From the **Settings** menu (gear icon), select **Partner settings**. On the **Account settings** page, select **App Management**. The App ID/Client ID is listed as the **Registered application App ID**. |
| Key | If you created a web app in the section [Enable API access](#enable-api-access), this is the key that you saved in step 5. |
| ドメイン | The domain for the integration sandbox. |

## <a name="run-tested-code"></a>Run tested code

To use your solution with real customer data, you must change from your integration sandbox credentials to your primary Partner account credentials.

When you're ready to use your tested code in your primary Partner account, you must get an Azure AD security token. This security token is based on your Partner Center app, key and domain (instead of your integration sandbox app, key and domain).

1. Follow the steps in [Partner Center authentication](partner-center-authentication.md) to get an Azure AD security token using your primary Partner Center credentials. (You previously followed these steps to get an Azure AD security token for your integration sandbox.)
2. Replace the integration security token in your code with the new security token for your primary Partner account.