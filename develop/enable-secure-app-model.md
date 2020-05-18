---
title: セキュリティで保護されたアプリケーション モデルを有効にする
description: パートナー センターとコントロール パネル アプリをセキュリティで保護します。
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 274b7ebc96cde1bca5c549fb92fe5ffb4ae29add
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155624"
---
# <a name="enabling-the-secure-application-model-framework"></a>セキュリティで保護されたアプリケーション モデル フレームワークを有効にする

**適用対象:**

- パートナー センター

Microsoft では、Microsoft Azure 多要素認証 (MFA) アーキテクチャを介してクラウド ソリューション プロバイダー (CSP) パートナーとコントロール パネル ベンダー (CPV) を認証することができる、セキュリティで保護されたスケーラブルなフレームワークを導入しています。

新しいモデルを使用して、Partner Center API の統合呼び出しのセキュリティを強化できます。 これは、すべてのパーティ (Microsoft、CSP パートナー、CPV など) がインフラストラクチャと顧客データをセキュリティ リスクから保護するために役立ちます。

## <a name="scope"></a>スコープ

この記事では、次のアクターについて説明します。

- CPV
  - CPV とは、Partner Center API と統合するために CSP パートナーによって使用されるアプリを開発する独立系ソフトウェア ベンダーです。
  - CPV は、パートナー センター ダッシュボードまたは API に直接アクセスできる CSP パートナーではありません。

- アプリ ID とユーザー認証を使用し、Partner Center API と直接統合する CSP 間接プロバイダーと CSP ダイレクト パートナー。

## <a name="security-requirements"></a>セキュリティ要件

セキュリティ要件の詳細については、「[パートナーのセキュリティ要件](https://docs.microsoft.com/partner-center/partner-security-requirements)」を参照してください。

## <a name="secure-application-model"></a>セキュリティで保護されたアプリケーション モデル

Marketplace アプリケーションでは、Microsoft API を呼び出すために CSP パートナーの特権を借用する必要があります。 このような機密性の高いアプリケーションに対するセキュリティ攻撃は、顧客データの侵害につながる可能性があります。

新しい認証フレームワークの概要と詳細については、[セキュア アプリケーション モデル フレームワーク](https://assetsprod.microsoft.com/secure-application-model-guide.pdf)のドキュメントをダウンロードします。 このドキュメントでは、Marketplace アプリケーションを持続可能にして、セキュリティ侵害に対して堅牢にするための原則とベスト プラクティスが説明されています。

## <a name="samples"></a>サンプル

次の概要ドキュメントとサンプル コードでは、パートナーがセキュア アプリケーション モデル フレームワークを実装する方法が説明されています。

- [CPV の概要ドキュメント](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [CSP の概要ドキュメント](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [.NET のサンプル](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Java のサンプル](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [REST の手順とサンプル](#rest)
- [PowerShell の手順とサンプル](#powershell)

## <a name="rest"></a>REST

サンプル コードを使用してセキュア アプリケーション モデル フレームワークで REST 呼び出しを行うには、次の手順を行います。

1. [Web アプリを作成する](#create-a-web-app)

2. [認証コードを取得する](#get-authorization-code)

3. [更新トークンを取得する](#get-refresh-token)

4. [アクセス トークンを取得する](#get-access-token)

5. [Partner Center API の呼び出しを行う](#make-partner-center-api-calls)

> [!TIP]
> Partner Center PowerShell モジュールを使用して、認証コードと更新トークンを取得できます。 手順 2 と 3 の代わりにこのオプションを選択できます。 詳細については、[PowerShell のセクションと例](#powershell)に関する記事を参照してください。

### <a name="create-a-web-app"></a>Web アプリを作成する

REST 呼び出しを行う前に、パートナー センターで Web アプリを作成して登録する必要があります。

1. [Azure portal](https://portal.azure.com) にサインインします。

2. Azure Active Directory (Azure AD) アプリを作成します。

3. *アプリケーションの要件に応じて*、委任されたアプリケーションのアクセス許可を次のリソースに付与します。 必要に応じて、アプリケーション リソースに委任されたアクセス許可をさらに追加することができます。

   1. **Microsoft パートナー センター** (一部のテナントでは、これが **SampleBECApp** と表示されます)

   2. **Azure Management API** (Azure API の呼び出しを計画している場合)

   3. **Windows Azure Active Directory**

4. アプリのホーム URL が、ライブ Web アプリが実行されているエンドポイントに設定されていることを確認します。 このアプリでは、Azure AD のログイン呼び出しから[認証コード](#get-authorization-code)を受け入れる必要があります。 たとえば、[次のセクション](#get-authorization-code)のサンプル コードでは、Web アプリが `https://localhost:44395/` で実行されています。

5. Azure AD の Web アプリの設定のうち、次の情報に注意してください。

   - アプリケーション ID
   - アプリケーション シークレット

> [!NOTE]
> [アプリケーション シークレットとして証明書を使用する](https://docs.microsoft.com/azure/active-directory/develop/active-directory-certificate-credentials)ことをお勧めします。 ただし、Azure portal でアプリケーション キーを作成することもできます。 [次のセクション](#get-authorization-code)のサンプル コードではアプリケーション キーを使用しています。

### <a name="get-authorization-code"></a>認証コードを取得する

Web アプリが Azure AD のログイン呼び出しから同意するには、次の認証コードを取得する必要があります。

1. [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) の URL で Azure AD にログインします。 必ず、Partner Center API の呼び出しを行うユーザー アカウント (管理エージェントや販売エージェント アカウントなど) を使用してログインしてください。

2. **Application-Id** を Azure AD アプリ ID (GUID) に置き換えます。

3. プロンプトが表示されたら、MFA が構成されたユーザー アカウントを使用してログインします。

4. プロンプトが表示されたら、追加の MFA 情報 (電話番号またはメール アドレス) を入力して、ログインを確認します。

5. ログインすると、ブラウザーによって Web アプリ エンドポイントへの呼び出しが認証コードと共にリダイレクトされます。 たとえば、次のサンプル コードを実行すると、`https://localhost:44395/` にリダイレクトされます。

#### <a name="authorization-code-call-trace"></a>認証コード呼び出しのトレース

```http
POST https://localhost:44395/ HTTP/1.1
Origin: https://login.microsoftonline.com
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Referrer: https://login.microsoftonline.com/kmsi
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: OpenIdConnect.nonce.hOMjjrivcxzuI4YqAw4uYC%2F%2BILFk4%2FCx3kHTHP3lBvA%3D=dHVyRXdlbk9WVUZFdlFONVdiY01nNEpUc0JRR0RiYWFLTHhQYlRGNl9VeXJqNjdLTGV3cFpIWFg1YmpnWVdQUURtN0dvMkdHS2kzTm02NGdQS09veVNEbTZJMDk1TVVNYkczYmstQmlKUzFQaTBFMEdhNVJGVHlES2d3WGlCSlVlN1c2UE9sd2kzckNrVGN2RFNULWdHY2JET3RDQUxSaXRfLXZQdG00RnlUM0E1TUo1YWNKOWxvQXRwSkhRYklQbmZUV3d3eHVfNEpMUUthMFlQUFgzS01RS2NvMXYtbnV4UVJOYkl4TTN0cw%3D%3D

code=AuthorizationCodeValue&id_token=IdTokenValue&<rest of properties for state>
```

### <a name="get-refresh-token"></a>更新トークンを取得する

次に、認証コードを使用して更新トークンを取得する必要があります。

1. 認証コードを使用して Azure AD ログイン エンドポイント `https://login.microsoftonline.com/CSPTenantID/oauth2/token` への POST 呼び出しを行います。 例については、次の[サンプル呼び出し](#sample-refresh-call)を参照してください。

2. 返される更新トークンに注意してください。

3. 更新トークンを Azure Key Vault に格納します。 詳細については、[Key Vault API のドキュメント](https://docs.microsoft.com/rest/api/keyvault/)を参照してください。

> [!IMPORTANT]
> 更新トークンは、Key Vault に[シークレットとして格納する](https://docs.microsoft.com/rest/api/keyvault/setsecret/setsecret)必要があります。

#### <a name="sample-refresh-call"></a>更新呼び出しのサンプル

プレースホルダー要求:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

要求本文:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

プレースホルダーの応答:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

応答本文:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a>アクセス トークンを取得する

Partner Center API の呼び出しを行う前に、アクセス トークンを取得する必要があります。 通常、アクセス トークンの有効期間は非常に限られているため (たとえば、1 時間未満)、更新トークンを使用してアクセス トークンを取得する必要があります。

プレースホルダー要求:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

要求本文:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

プレースホルダーの応答:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

応答本文:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a>Partner Center API の呼び出しを行う

Partner Center API を呼び出すには、アクセス トークンを使用する必要があります。 次の呼び出し例を参照してください。

#### <a name="example-partner-center-api-call"></a>Partner Center API の呼び出し例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

[Partner Center PowerShell モジュール](https://www.powershellgallery.com/packages/PartnerCenter)を使用すると、アクセス トークンの認証コードを交換するために必要なインフラストラクチャを減らすことができます。 この方法は、[Partner Center REST 呼び出し](#rest)を行う場合に省略可能です。

このプロセスの詳細については、[セキュリティで保護されたアプリ モデル](https://docs.microsoft.com/powershell/partnercenter/secure-app-model)の PowerShell ドキュメントを参照してください。

1. Azure AD モジュールと Partner Center PowerShell モジュールをインストールします。

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. **[New-PartnerAccessToken](https://docs.microsoft.com/powershell/module/partnercenter/new-partneraccesstoken)** コマンドを使用して同意プロセスを実行し、必要な更新トークンをキャプチャします。

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > 種類が **Web/API** の Azure AD アプリが使用されているため、**New-PartnerAccessToken** コマンドに **ServicePrincipal** パラメーターが使用されています。 この種類のアプリでは、クライアント識別子とシークレットをアクセス トークン要求に含める必要があります。 **Get-Credential** コマンドが呼び出されると、ユーザー名とパスワードの入力を求められます。 ユーザー名としてアプリケーション識別子を入力します。 パスワードとしてアプリケーション シークレットを入力します。 **New-PartnerAccessToken** コマンドが呼び出されると、資格情報の再入力を求めるプロンプトが表示されます。 使用しているサービス アカウントの資格情報を入力します。 このサービス アカウントは、適切なアクセス許可を持つパートナー アカウントである必要があります。

3. 更新トークンの値をコピーします。

    ```powershell
    $token.RefreshToken | clip
    ```

更新トークンの値は、Azure Key Vault などの安全なリポジトリに格納するようにします。 PowerShell を使用してセキュリティで保護されたアプリケーション モジュールを利用する方法の詳細については、[多要素認証](https://docs.microsoft.com/powershell/partnercenter/multi-factor-auth)の記事を参照してください。
