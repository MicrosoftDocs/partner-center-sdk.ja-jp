---
title: パートナー センターの認証
description: パートナー センターでは認証に Azure AD を使用するため、パートナー センター API を使用するには、認証設定を正しく構成する必要があります。
ms.assetid: 2307F2A8-7BD4-4442-BEF7-F065F16DA0B2
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 36292ac800f7722ce3b5b95c8af19e4690f60ad9
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157104"
---
# <a name="partner-center-authentication"></a>パートナー センターの認証

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナー センターでは認証に Azure Active Directory を使用します。 パートナー センター API、SDK、または PowerShell モジュールと対話する場合は、Azure AD アプリケーションを正しく構成してから、アクセス トークンを要求する必要があります。 パートナー センターでは、アプリのみの認証、またはアプリとユーザー認証を使用して取得したアクセス トークンを使用できます。 ただし、考慮する必要がある重要な項目が 2 つあります。

- アプリとユーザー認証を使用してパートナー センター API にアクセスする場合は、多要素認証を使用します。 この変更に関する詳細については、[セキュリティで保護されたアプリケーション モデルの有効化](enable-secure-app-model.md)に関する記事をご覧ください。

- 一部の操作については、パートナー センター API はアプリのみの認証をサポートしていません。 アプリとユーザー認証を使用する必要がある特定のシナリオがあります。 「[シナリオ](https://docs.microsoft.com/partner-center/develop/scenarios)」の各記事にある見出し "*前提条件*" の下に、アプリのみの認証、アプリとユーザー認証、またはその両方がサポートされているかどうかを明示するドキュメントが示されています。

## <a name="initial-setup"></a>初期セットアップ

1. 最初に、プライマリ パートナー センター アカウントと統合サンドボックス パートナー センター アカウントの両方があることを確認する必要があります。 詳しくは、「[パートナー センターのアカウントで API アクセスを設定する](set-up-api-access-in-partner-center.md)」をご覧ください。 プライマリ アカウントと統合サンドボックス アカウントの両方について、Azure AAD アプリの登録 ID とシークレットをメモしておきます (アプリのみの識別にはクライアント シークレットが必要です)。

2. Azure portal から Azure AD にサインインします。 **[他のアプリケーションに対するアクセス許可]** で、**Windows Azure Active Directory** のアクセス許可を **[委任されたアクセス許可]** に設定し、 **[サインインしたユーザーとしてディレクトリにアクセスします]** と **[サインインとユーザー プロファイルの読み取り]** の両方を選択します。

3. Azure portal で、 **[アプリケーションの追加]** を選択します。 Microsoft パートナー センター アプリケーションである "Microsoft パートナー センター" を検索します。 **[委任されたアクセス許可]** を **[Access Partner Center API]\(パートナー センター API へのアクセス\)** に設定します。 Microsoft Cloud Germany のパートナー センターまたは Microsoft Cloud for US Government のパートナー センターを使用している場合、この手順は必須です。 パートナー センターのグローバル インスタンスを使用している場合、この手順は省略可能です。 CSP パートナーは、パートナー センター ポータルのアプリ管理機能を使用して、パートナー センターのグローバル インスタンスに対してこの手順を省略できます。

## <a name="app-only-authentication"></a>アプリのみの認証

アプリのみの認証を使用してパートナー センター REST API、.NET API、Java API、または PowerShell モジュールにアクセスしたい場合は、次の説明を使用してそのようにできます。

## <a name="net-app-only-authentication"></a>.NET (アプリのみの認証)

```csharp
public static IAggregatePartner GetPartnerCenterTokenUsingAppCredentials()
{
    IPartnerCredentials partnerCredentials =
        PartnerCredentials.Instance.GenerateByApplicationCredentials(
            PartnerApplicationConfiguration.ApplicationId,
            PartnerApplicationConfiguration.ApplicationSecret,
            PartnerApplicationConfiguration.ApplicationDomain);

    // Create operations instance with partnerCredentials.
    return PartnerService.Instance.CreatePartnerOperations(partnerCredentials);
}
```

## <a name="java-app-only-authentication"></a>Java (アプリのみの認証)

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

```java
public IAggregatePartner getAppPartnerOperations()
{
    IPartnerCredentials appCredentials =
        PartnerCredentials.getInstance().generateByApplicationCredentials(
        PartnerApplicationConfiguration.getApplicationId(),
        PartnerApplicationConfiguration.getApplicationSecret(),
        PartnerApplicationConfiguration.getApplicationDomain());

    return PartnerService.getInstance().createPartnerOperations( appCredentials );
}
```

## <a name="rest-app-only-authentication"></a>REST (アプリのみの認証)

### <a name="rest-request"></a>REST 要求

```http
POST https://login.microsoftonline.com/{tenantId}/oauth2/token HTTP/1.1
Accept: application/json
return-client-request-id: true
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Host: login.microsoftonline.com
Content-Length: 194
Expect: 100-continue

resource=https%3A%2F%2Fgraph.windows.net&client_id={client-id-here}&client_secret={client-secret-here}&grant_type=client_credentials
```

### <a name="rest-response"></a>REST 応答

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a>アプリとユーザー認証

これまで、[リソース所有者のパスワード資格情報の付与](https://tools.ietf.org/html/rfc6749#section-4.3)は、パートナー センター REST API、.NET API、Java API、または PowerShell モジュールで使用するアクセス トークンを要求するために使用されてきました。 この方法は、クライアント識別子とユーザー資格情報を使用して Azure Active Directory にアクセス トークンを要求するために使用されていました。 しかし、パートナー センターでは、アプリとユーザー認証を使用する場合に多要素認証が必要になるため、このアプローチは機能しなくなります。 この要件に準拠するために、Microsoft では、多要素認証を使用するクラウド ソリューション プロバイダー (CSP) パートナーおよびコントロール パネル ベンダー (CPV) を認証するための、セキュリティで保護されたスケーラブルなフレームワークを導入しています。 このフレームワークは、セキュア アプリケーション モデルと呼ばれ、同意プロセスと、更新トークンを使用したアクセス トークンの要求で構成されています。

### <a name="partner-consent"></a>パートナーの同意

パートナーの同意プロセスは、パートナーが多要素認証を使用して認証を行い、アプリケーションに同意し、更新トークンが Azure Key Vault のようなセキュリティで保護されたリポジトリに格納される、対話型のプロセスです。 このプロセスには、統合のための専用アカウントを使用することをお勧めします。

> [!IMPORTANT]
> パートナーの同意プロセスで使用されるサービス アカウントに対して、適切な多要素認証ソリューションを有効にする必要があります。 そうしない場合、結果として得られる更新トークンは、セキュリティ要件に準拠しなくなります。

### <a name="samples-for-app--user-authentication"></a>アプリとユーザー認証のサンプル

パートナーの同意プロセスは、さまざまな方法で実行できます。 必要な各操作の実行方法をパートナーの方々が理解するための一助として、次のサンプルを開発しました。 お使いの環境に適切なソリューションを実装する際には、コーディング標準とセキュリティ ポリシーに準拠したソリューションを開発することが重要です。

## <a name="net-appuser-authentication"></a>.NET (アプリとユーザー認証)

[パートナーの同意](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault)サンプル プロジェクトでは、ASP.NET を使用して開発された Web サイトを利用して、同意を取得し、更新トークンを要求してから、それを Azure Key Vault に安全に格納する方法を示しています。 このサンプルに必要な前提条件を作成するには、次の手順を実行します。

1. Azure portal または次の PowerShell コマンドを使用して、Azure Key Vault のインスタンスを作成します。 このコマンドを実行する前に、必ずパラメーター値を適宜変更してください。 コンテナー名は一意である必要があります。

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Azure Key Vault の作成の詳細については、「[クイック スタート: Azure portal を使用して Azure Key Vault との間でシークレットの設定と取得を行う](https://docs.microsoft.com/azure/key-vault/quick-create-portal)」または「[クイック スタート: PowerShell を使用して Azure Key Vault との間でシークレットの設定と取得を行う](https://docs.microsoft.com/azure/key-vault/quick-create-powershell)」を参照してください。 次に、シークレットを設定して取得します。

2. Azure portal または次のコマンドを使用して、Azure AD アプリケーションとキーを作成します。

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    アプリケーション識別子とシークレットの値は、以下の手順で使用するため、必ずメモしておいてください。

3. Azure portal または次のコマンドを使用して、新しく作成された Azure AD アプリケーションにシークレットの読み取りアクセス許可を付与します。

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. パートナー センター用に構成された Azure AD アプリケーションを作成します。 この手順を完了するには、次の操作を実行します。

    - パートナー センター ダッシュボードの[アプリ管理](https://partner.microsoft.com/pcv/apiintegration/appmanagement)機能に移動します。
    - *[新しい Web アプリの追加]* をクリックして、新しい Azure AD アプリケーションを作成します。

    "*アプリ ID*"、*アカウント ID**、および "*キー*" の値は、以下の手順で使用するため、必ず文書化してください。

5. Visual Studio または次のコマンドを使用して、[Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) リポジトリを複製します。

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. `Partner-Center-DotNet-Samples\secure-app-model\keyvault` ディレクトリにある *PartnerConsent* プロジェクトを開きます。

7. [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config) にあるアプリケーション設定にデータを入力します。

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!--
        Endpoint address for the instance of Azure KeyVault. This is
        the DNS Name for the instance of Key Vault that you provisioned.
     -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- App ID that is given access for KeyVault to store refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate
        to your environment. The following application secret is for sample
        application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

    > [!IMPORTANT]
    > アプリケーション シークレットなどの機密情報は、構成ファイルに格納しないでください。 ここでそれを行ったのは、これがサンプル アプリケーションであるためです。 実稼働アプリケーションでは、証明書ベースの認証を使用することを強くお勧めします。 詳細については、[アプリケーション認証用の証明書資格情報](https://docs.microsoft.com/azure/active-directory/develop/active-directory-certificate-credentials)に関する記事を参照してください。

8. このサンプル プロジェクトを実行すると、認証を求めるメッセージが表示されます。 正常に認証されると、Azure AD でアクセス トークンが要求されます。 Azure AD から返される情報には、Azure Key Vault の構成済みインスタンスに格納される更新トークンが含まれています。

## <a name="java-appuser-authentication"></a>Java (アプリとユーザー認証)

[パートナーの同意](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault)サンプル プロジェクトでは、JSP を使用して開発された Web サイトを利用して、同意を取得し、更新トークンを要求してから、それを Azure Key Vault に安全に格納する方法を示しています。 このサンプルに必要な前提条件を作成するには、以下を実行します。

1. Azure portal または次の PowerShell コマンドを使用して、Azure Key Vault のインスタンスを作成します。 このコマンドを実行する前に、必ずパラメーター値を適宜変更してください。 コンテナー名は一意である必要があります。

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Azure Key Vault の作成の詳細については、「[クイック スタート: Azure portal を使用して Azure Key Vault との間でシークレットの設定と取得を行う](https://docs.microsoft.com/azure/key-vault/quick-create-portal)」または「[クイック スタート: PowerShell を使用して Azure Key Vault との間でシークレットの設定と取得を行う](https://docs.microsoft.com/azure/key-vault/quick-create-powershell)」を参照してください。

2. Azure portal または次のコマンドを使用して、Azure AD アプリケーションとキーを作成します。

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    アプリケーション識別子とシークレットの値は、以下の手順で使用するため、必ず文書化してください。

3. Azure portal または次のコマンドを使用して、新しく作成された Azure AD アプリケーションにシークレットの読み取りアクセス許可を付与します。

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. パートナー センター用に構成された Azure AD アプリケーションを作成します。 この手順を完了するには、以下を実行します。

    - パートナー センター ダッシュボードの[アプリ管理](https://partner.microsoft.com/pcv/apiintegration/appmanagement)機能に移動します。
    - *[新しい Web アプリの追加]* をクリックして、新しい Azure AD アプリケーションを作成します。

    "*アプリ ID*"、*アカウント ID**、および "*キー*" の値は、以下の手順で使用するため、必ず文書化してください。

5. 次のコマンドを使用して、[Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) リポジトリを複製します

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. `Partner-Center-Java-Samples\secure-app-model\keyvault` ディレクトリにある *PartnerConsent* プロジェクトを開きます。

7. [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) ファイルにあるアプリケーション設定にデータを入力します。

    ```xml
    <filter>
        <filter-name>AuthenticationFilter</filter-name>
        <filter-class>com.microsoft.store.samples.partnerconsent.security.AuthenticationFilter</filter-class>
        <init-param>
            <param-name>client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_base_url</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_certifcate_path</param-name>
            <param-value></param-value>
        </init-param>
    </filter>
    ```

    > [!IMPORTANT]
    > アプリケーション シークレットなどの機密情報は、構成ファイルに格納しないでください。 ここでそれを行ったのは、これがサンプル アプリケーションであるためです。 実稼働アプリケーションでは、証明書ベースの認証を使用することを強くお勧めします。 詳細については、[Key Vault 証明書認証](https://github.com/Azure-Samples/key-vault-java-certificate-authentication)に関するページを参照してください。

8. このサンプル プロジェクトを実行すると、認証を求めるメッセージが表示されます。 正常に認証されると、Azure AD でアクセス トークンが要求されます。 Azure AD から返される情報には、Azure Key Vault の構成済みインスタンスに格納される更新トークンが含まれています。

## <a name="cloud-solution-provider-authentication"></a>クラウド ソリューション プロバイダー認証

クラウド ソリューション プロバイダー パートナーは、[パートナーの同意](#partner-consent)プロセスを通じて取得した更新トークンを使用できます。

### <a name="samples-for-cloud-solution-provider-authentication"></a>クラウド ソリューション プロバイダー認証のサンプル

必要な各操作の実行方法をパートナーの方々が理解するための一助として、次のサンプルを開発しました。 お使いの環境に適切なソリューションを実装する際には、コーディング標準とセキュリティ ポリシーに準拠したソリューションを開発することが重要です。

## <a name="net-csp-authentication"></a>.NET (CSP 認証)

1. まだ実行していない場合は、[パートナーの同意プロセス](#partner-consent)を実行します。

2. Visual Studio または次のコマンドを使用して、[Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) リポジトリを複製します

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. `Partner-Center-DotNet-Samples\secure-app-model\keyvault` ディレクトリにある `CSPApplication` プロジェクトを開きます。

4. [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) ファイルにあるアプリケーション設定を更新します。

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) ファイルにある **PartnerId** および **CustomerId** 変数に適切な値を設定します。

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. このサンプル プロジェクトは、実行すると、パートナーの同意プロセス中に取得された更新トークンを取得します。 これは次に、パートナーの代わりにパートナー センター SDK と対話するためのアクセス トークンを要求します。 最後に、指定された顧客に代わって Microsoft Graph と対話するためのアクセス トークンを要求します。

## <a name="java-csp-authentication"></a>Java (CSP 認証)

1. まだ実行していない場合は、[パートナーの同意プロセス](#partner-consent)を実行します。

2. Visual Studio または次のコマンドを使用して、[Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) リポジトリを複製します

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. `Partner-Center-Java-Samples\secure-app-model\keyvault` ディレクトリにある `cspsample` プロジェクトを開きます。

4. [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) ファイルにあるアプリケーション設定を更新します。

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. このサンプル プロジェクトは、実行すると、パートナーの同意プロセス中に取得された更新トークンを取得します。 これは次に、パートナーの代わりにパートナー センター SDK と対話するためのアクセス トークンを要求します。

6. 省略可能 - 顧客に代わって Azure Resource Manager および Microsoft Graph と対話する方法を確認する場合は、*RunAzureTask* と *RunGraphTask* 関数呼び出しのコメントを解除します。

## <a name="control-panel-provider-authentication"></a>コントロール パネル プロバイダー認証

コントロール パネル ベンダーは、サポートを提供する対象の各パートナーに[パートナーの同意](#partner-consent)プロセスを実行してもらう必要があります。 これが完了すると、そのプロセスを通じて取得された更新トークンを使用して、パートナー センター REST API と .NET API にアクセスします。

### <a name="samples-for-cloud-panel-provider-authentication"></a>クラウド パネル プロバイダー認証のサンプル

必要な各操作の実行方法をコントロール パネル ベンダーの方々が理解するための一助として、次のサンプルを開発しました。 お使いの環境に適切なソリューションを実装する際には、コーディング標準とセキュリティ ポリシーに準拠したソリューションを開発することが重要です。

## <a name="net-cpv-authentication"></a>.NET (CPV 認証)

1. 適切な同意を得るために、クラウド ソリューション プロバイダー パートナー向けのプロセスを開発してデプロイします。 詳細と例については、「[パートナーの同意](#partner-consent)」を参照してください。

    > [!IMPORTANT]
    > クラウド ソリューション プロバイダー パートナーからのユーザー資格情報は格納しないでください。 パートナーの同意プロセスを通じて取得した更新トークンは、保存し、Microsoft API と対話するためのアクセス トークンを要求するために使用する必要があります。

2. Visual Studio または次のコマンドを使用して、[Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) リポジトリを複製します

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. `Partner-Center-DotNet-Samples\secure-app-model\keyvault` ディレクトリにある `CPVApplication` プロジェクトを開きます。

4. [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) ファイルにあるアプリケーション設定を更新します。

    ```xml
    <!-- AppID that represents Control panel vendor application -->
    <add key="ida:CPVApplicationId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CPVApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) ファイルにある **PartnerId** および **CustomerId** 変数に適切な値を設定します。

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. このサンプル プロジェクトは、実行すると、指定されたパートナーの更新トークンを取得します。 これは次に、パートナーに代わってパートナー センターと Azure AD Graph にアクセスするためのアクセス トークンを要求します。 これが次に実行するタスクは、顧客テナントに対するアクセス許可付与の削除と作成です。 コントロール パネル ベンダーと顧客の間に関係がないため、パートナー センター API を使用してこれらのアクセス許可を追加する必要があります。 次の例は、これがどのように行われるかを示しています。

    ```csharp
    JObject contents = new JObject
    {
        // Provide your application display name
        ["displayName"] = "CPV Marketplace",

        // Provide your application id
        ["applicationId"] = CPVApplicationId,

        // Provide your application grants
        ["applicationGrants"] = new JArray(
            JObject.Parse("{\"enterpriseApplicationId\": \"00000002-0000-0000-c000-000000000000\", \"scope\":\"Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All\"}"), // for Azure AD Graph access,  Directory.Read.All
            JObject.Parse("{\"enterpriseApplicationId\": \"797f4846-ba00-4fd7-ba43-dac1f8f63013\", \"scope\":\"user_impersonation\"}")) // for Azure Resource Manager access
    };

    /**
     * The following steps have to be performed once per customer tenant if your application is
     * a control panel vendor application and requires customer tenant Azure AD Graph access.
     **/

    // delete the previous grant into customer tenant
    JObject consentDeletion = await ApiCalls.DeleteAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents/{1}", CustomerId, CPVApplicationId));

    // create new grants for the application given the setting in application grants payload.
    JObject consentCreation = await ApiCalls.PostAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents", CustomerId),
        contents.ToString());
    ```

これらのアクセス許可が確立されると、このサンプルは顧客に代わって Azure AD Graph を使用して操作を実行します。

## <a name="java-cpv-authentication"></a>Java (CPV 認証)

1. 適切な同意を得るために、クラウド ソリューション プロバイダー パートナー向けのプロセスを開発してデプロイします。 詳細と例については、「[パートナーの同意](#partner-consent)」を参照してください。

    > [!IMPORTANT]
    > クラウド ソリューション プロバイダー パートナーからのユーザー資格情報は格納しないでください。 パートナーの同意プロセスを通じて取得した更新トークンは、保存し、Microsoft API と対話するためのアクセス トークンを要求するために使用する必要があります。

2. 次のコマンドを使用して、[Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) リポジトリを複製します

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. `Partner-Center-Java-Samples\secure-app-model\keyvault` ディレクトリにある `cpvsample` プロジェクトを開きます。

4. [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) ファイルにあるアプリケーション設定を更新します。

    ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    partnercenter.displayName=
    ```

    `partnercenter.displayName` の値は、お使いのマーケットプレース アプリケーションの表示名にする必要があります。

5. [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) ファイルにある **partnerId** および **customerId** 変数に適切な値を設定します。

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. このサンプル プロジェクトは、実行すると、指定されたパートナーの更新トークンを取得します。 これは次に、パートナーに代わってパートナー センターにアクセスするためのアクセス トークンを要求します。 これが次に実行するタスクは、顧客テナントに対するアクセス許可付与の削除と作成です。 コントロール パネル ベンダーと顧客の間に関係がないため、パートナー センター API を使用してこれらのアクセス許可を追加する必要があります。 次の例は、アクセス許可を付与する方法を示しています。

    ```java
    ApplicationGrant azureAppGrant = new ApplicationGrant();

    azureAppGrant.setEnterpriseApplication("797f4846-ba00-4fd7-ba43-dac1f8f63013");
    azureAppGrant.setScope("user_impersonation");

    ApplicationGrant graphAppGrant = new ApplicationGrant();

    graphAppGrant.setEnterpriseApplication("00000002-0000-0000-c000-000000000000");
    graphAppGrant.setScope("Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All");

    ApplicationConsent consent = new ApplicationConsent();

    consent.setApplicationGrants(Arrays.asList(azureAppGrant, graphAppGrant));
    consent.setApplicationId(properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID));
    consent.setDisplayName(properties.getProperty(PropertyName.PARTNER_CENTER_DISPLAY_NAME));

    // Deletes the existing grant into the customer it is present.
    partnerOperations.getServiceClient().delete(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents/{1}",
            customerId,
            properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID)));

    // Consent to the defined applications and the respective scopes.
    partnerOperations.getServiceClient().post(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents",
            customerId),
        consent);
    ```

顧客に代わって Azure Resource Manager および Microsoft Graph と対話する方法を確認する場合は、*RunAzureTask* と *RunGraphTask* 関数呼び出しのコメントを解除します。
