---
title: セキュリティで保護されたアプリケーションモデルを有効にする
description: パートナーセンターとコントロールパネルアプリをセキュリティで保護します。
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: c8700ecdf42b0a5e156d68854674c904d8da1d4c
ms.sourcegitcommit: 7e5e3590931010eb0e0fef3e7f6d5d7d084a69ba
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74995137"
---
# <a name="enabling-the-secure-application-model-framework"></a>セキュリティで保護されたアプリケーションモデルフレームワークを有効にする

適用対象:

- パートナー センター

Microsoft では、Microsoft Azure multi-factor authentication (MFA) アーキテクチャを使用して、クラウドソリューションプロバイダー (CSP) パートナーとコントロールパネルベンダー (CPV) を認証するための、セキュリティで保護されたスケーラブルなフレームワークを導入しています。

新しいモデルを使用して、パートナーセンターの API 統合呼び出しのセキュリティを昇格させることができます。 これにより、すべてのパーティ (Microsoft、CSP パートナー、CPVs など) がセキュリティ上のリスクからインフラストラクチャと顧客データを保護するのに役立ちます。

## <a name="scope"></a>適用範囲

このトピックでは、次のアクターについて説明します。

- CPVs
  - CPV は、パートナーセンター Api と統合するために CSP パートナーが使用するアプリを開発する独立系ソフトウェアベンダーです。
  - CPV は、パートナーセンターのダッシュボードまたは Api に直接アクセスする CSP パートナーではありません。
- アプリ ID とユーザー認証を使用し、パートナーセンター Api と直接統合された CSP 間接プロバイダーと CSP 直接パートナー。

## <a name="security-requirements"></a>セキュリティ要件

セキュリティ要件の詳細については、「[パートナーのセキュリティ要件](https://docs.microsoft.com/partner-center/partner-security-requirements)」を参照してください。

## <a name="secure-application-model"></a>セキュリティで保護されたアプリケーション モデル

Marketplace アプリケーションでは、Microsoft Api を呼び出すために CSP パートナーの特権を借用する必要があります。 これらの機密性の高いアプリケーションに対するセキュリティ攻撃によって、顧客データが侵害される可能性があります。

新しい認証フレームワークの概要と詳細については、[セキュリティで保護されたアプリケーションモデルフレームワーク](https://assetsprod.microsoft.com/secure-application-model-guide.pdf)に関するドキュメントをダウンロードしてください。 このドキュメントでは、marketplace アプリケーションをセキュリティ侵害から確実かつ堅牢にするための原則とベストプラクティスについて説明します。

## <a name="samples"></a>サンプル

次の概要ドキュメントとサンプルコードでは、パートナーがセキュリティで保護されたアプリケーションモデルフレームワークを実装する方法について説明します。

- [CPV の概要ドキュメント](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [CSP の概要ドキュメント](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [.NET のサンプル](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Java のサンプル](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

- [REST の手順とサンプル](#rest)
- [PowerShell の手順とサンプル](#powershell)

## <a name="rest"></a>REST

サンプルコードを使用して、セキュリティで保護されたアプリケーションモデルフレームワークで REST 呼び出しを行うには、次の操作を行う必要があります。

1. [Web アプリの作成](#create-a-web-app)
2. [認証コードを取得する](#get-authorization-code)
3. [更新トークンを取得する](#get-refresh-token)
4. [アクセストークンを取得する](#get-access-token)
5. [パートナーセンターの API 呼び出しを作成する](#make-partner-center-api-calls)

> [!TIP]
> パートナーセンターの PowerShell モジュールを使用して、認証コードと更新トークンを取得できます。 このオプションは、手順 2. と 3. の代わりに選択できます。 詳細については、 [PowerShell のセクションと例](#powershell)を参照してください。

### <a name="create-a-web-app"></a>Web アプリを作成する

REST 呼び出しを行う前に、パートナーセンターで web アプリを作成して登録する必要があります。

1. [Azure portal](https://portal.azure.com) にサインインします。
2. Azure Active Directory (Azure AD) アプリを作成します。
3. *アプリケーションの要件に応じて*、次のリソースへの委任されたアプリケーションアクセス許可を付与します。 必要に応じて、アプリケーションリソースに対して委任されたアクセス許可をさらに追加することができます。
    1. **Microsoft パートナーセンター** (一部のテナントはこれを**sampleて app**として示しています)
    2. **Azure 管理 api** (azure api の呼び出しを計画している場合)
    3. **Windows Azure Active Directory**
4. アプリのホーム URL が、ライブ web アプリが実行されているエンドポイントに設定されていることを確認します。 このアプリは、Azure AD ログイン呼び出しからの[認証コード](#get-authorization-code)を受け入れる必要があります。 たとえば、[次のセクション](#get-authorization-code)のコード例では、web アプリが `https://localhost:44395/`で実行されています。
5. Azure AD の web アプリの設定から次の情報を確認してください。
    - アプリケーション ID
    - アプリケーション シークレット

> [!NOTE]
> [アプリケーションシークレットとして証明書を使用](https://docs.microsoft.com/azure/active-directory/develop/active-directory-certificate-credentials)することをお勧めします。 ただし、Azure portal でアプリケーションキーを作成することもできます。 [次のセクション](#get-authorization-code)のサンプルコードでは、アプリケーションキーを使用します。

### <a name="get-authorization-code"></a>認証コードを取得する

Web アプリが Azure AD ログイン呼び出しから同意するには、次の認証コードを取得する必要があります。

1. 次の URL で Azure AD にログインします: <https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile>。 パートナーセンターの API 呼び出しを行うユーザーアカウント (管理エージェントや販売エージェントアカウントなど) を使用してログインしてください。
2. **アプリケーション id**を AZURE AD アプリ ID (GUID) に置き換えます。
3. プロンプトが表示されたら、MFA が構成されたユーザーアカウントでログインします。
4. プロンプトが表示されたら、追加の MFA 情報 (電話番号または電子メールアドレス) を入力して、ログインを確認します。
5. ログインすると、web アプリのエンドポイントへの呼び出しが、ブラウザーによって認証コードと共にリダイレクトされます。 たとえば、次のサンプルコードは `https://localhost:44395/`にリダイレクトします。

#### <a name="authorization-code-call-trace"></a>認証コード呼び出しトレース

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

### <a name="get-refresh-token"></a>更新トークンの取得

次に、認証コードを使用して更新トークンを取得する必要があります。

1. 認証コードを使用して `https://login.microsoftonline.com/CSPTenantID/oauth2/token` Azure AD ログインエンドポイントへの POST 呼び出しを行います。 例については、次の[サンプル呼び出し](#sample-refresh-call)を参照してください。
2. 返される更新トークンに注意してください。
3. 更新トークンを Azure Key Vault に格納します。 詳細については、 [KEY VAULT API のドキュメント](https://docs.microsoft.com/rest/api/keyvault/)を参照してください。

> [!IMPORTANT]
> 更新トークンは、Key Vault に[シークレットとして格納されて](https://docs.microsoft.com/rest/api/keyvault/setsecret/setsecret)いる必要があります。

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

パートナーセンター Api の呼び出しを行う前に、アクセストークンを取得する必要があります。 アクセストークンを取得するには、更新トークンを使用する必要があります。これは、一般に、アクセストークンの有効期間が非常に限られているためです (たとえば、1時間未満)。

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

### <a name="make-partner-center-api-calls"></a>パートナーセンターの API 呼び出しを行う

パートナーセンター Api を呼び出すには、アクセストークンを使用する必要があります。 次の呼び出し例を参照してください。

#### <a name="example-partner-center-api-call"></a>パートナーセンター API 呼び出しの例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

[パートナーセンターの PowerShell モジュール](https://www.powershellgallery.com/packages/PartnerCenter)を使用して、アクセストークンの認証コードを交換するために必要なインフラストラクチャを減らすことができます。 [パートナーセンターの REST 呼び出し](#rest)を行う場合、この方法は省略可能です。

このプロセスの詳細については、「[セキュリティで保護されたアプリモデル](https://docs.microsoft.com/powershell/partnercenter/secure-app-model)の PowerShell ドキュメント」を参照してください。

1. Azure AD とパートナーセンターの PowerShell モジュールをインストールします。

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. PowerShell を使用して、Azure AD アプリケーションの応答 URL として `urn:ietf:wg:oauth:2.0:oob` を追加します。 オブジェクト識別子パラメーターの値は、Azure AD アプリケーションのオブジェクト識別子に置き換えるようにしてください。 この値は、Azure 管理ポータルで確認できます。

    ```powershell
    Connect-AzureAD
    ```

    ```powershell
    Set-AzureADApplication -ObjectId 659dd68d-3414-4254-a48b-c081b5631b86 -ReplyUrls @("urn:ietf:wg:oauth:2.0:oob")
    ```

3. **[PartnerAccessToken](https://docs.microsoft.com/powershell/module/partnercenter/new-partneraccesstoken)** コマンドを使用して同意プロセスを実行し、必要な更新トークンをキャプチャします。

    ```powershell
    $credential = Get-Credential
    ```

    ```powershell
    $token = New-PartnerAccessToken -Consent -Credential $credential -Resource https://api.partnercenter.microsoft.com -ServicePrincipal
    ```

    > [!NOTE]
    > **PartnerAccessToken**コマンドで**serviceprincipal**パラメーターを使用しているのは、種類が**web/API**の Azure AD アプリが使用されているためです。 この種類のアプリでは、アクセストークン要求にクライアント識別子とシークレットが含まれている必要があります。

4. 更新トークンの値をコピーします。

    ```powershell
    $token.RefreshToken | clip
    ```

5. **Get Credential**コマンドが呼び出されると、ユーザー名とパスワードを入力するように求められます。 アプリケーション識別子をユーザー名として入力します。 アプリケーションシークレットをパスワードとして入力します。

6. **PartnerAccessToken**コマンドが呼び出されると、資格情報をもう一度入力するように求められます。 使用しているサービスアカウントの資格情報を入力します。 このサービスアカウントは、apppropriate アクセス許可を持つパートナーアカウントである必要があります。

7. **PartnerAccessToken**が正常に実行されると、 **$token**変数に Azure AD からの応答が含まれるようになります。 更新トークンの値は、必ず、Azure Key Vault などのセキュリティで保護されたリポジトリに保存してください。
