---
title: パートナーセンターの認証
description: パートナーセンターは認証に Azure AD を使用し、パートナーセンター Api を使用するには、認証設定を正しく構成する必要があります。
ms.assetid: 2307F2A8-7BD4-4442-BEF7-F065F16DA0B2
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7a29d178774f301f5f3030df119bf30953fa0d8f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486982"
---
# <a name="partner-center-authentication"></a>パートナーセンターの認証

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーセンターでは、認証に Azure Active Directory を利用します。 パートナーセンターの API、SDK、または PowerShell モジュールと対話する場合は、Azure AD アプリケーションを正しく構成してから、アクセストークンを要求する必要があります。 パートナーセンターでは、app only または app + user 認証を使用して取得したアクセストークンを使用できます。 ただし、考慮する必要がある重要な項目が2つあります。

- アプリ + ユーザー認証を使用してパートナーセンター API にアクセスするときは、multi-factor authentication を使用する必要があります。 この変更に関する詳細については、「[セキュリティで保護されたアプリケーションモデルの有効化](enable-secure-app-model.md)」を参照してください。
- 一部の操作では、パートナーセンター API はアプリ専用認証をサポートしています。 これは、アプリとユーザー認証を使用する必要がある特定のシナリオがあることを意味します。 各[シナリオ](https://docs.microsoft.com/partner-center/develop/scenarios)の記事の*前提条件*の見出しの下に、アプリ専用認証、アプリ + ユーザー認証、またはその両方がサポートされているかどうかを示すドキュメントがあります。

## <a name="initial-setup"></a>初期セットアップ

1. まず、プライマリパートナーセンターアカウントと統合サンドボックスパートナーセンターアカウントの両方があることを確認する必要があります。 詳しくは、「[パートナー センターのアカウントで API アクセスを設定する](set-up-api-access-in-partner-center.md)」をご覧ください。 プライマリアカウントと統合サンドボックスアカウントの両方について、Azure AAD アプリの登録 ID とシークレット (アプリ専用の id にはクライアントシークレットが必要) をメモしておきます。

2. Azure 管理ポータルから Azure AD にサインインします。 **[他のアプリケーションに対するアクセス]** 許可 で、 **Windows Azure Active Directory**のアクセス許可を 委任された **[アクセス許可]** に設定し、サインイン **[ユーザーとしてディレクトリにアクセス]** する と **[サインインとユーザープロファイルの読み取り]** の両方を選択します。

3. Azure 管理ポータルで、**アプリケーションを追加**します。 Microsoft パートナーセンターアプリケーションである "Microsoft パートナーセンター" を検索します。 **パートナーセンター API にアクセス**するための委任された**アクセス許可**を設定します。 米国政府機関向けの Microsoft Cloud にパートナーセンター Microsoft Cloud ドイツまたはパートナーセンターを使用している場合、この手順は必須です。 パートナーセンターのグローバルインスタンスを使用している場合、この手順は省略可能です。 CSP パートナーは、パートナーセンターポータルのアプリ管理機能を使用して、パートナーセンターのグローバルインスタンスに対してこの手順を省略できます。

## <a name="app-only-authentication"></a>アプリのみの認証

パートナーセンター REST API、.NET API、Java API、または PowerShell モジュールにアクセスするためにアプリ専用認証を使用する場合は、次の手順を利用して実行できます。

### <a name="net-app-only-authentication"></a>.NET (アプリ専用認証)

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

### <a name="java-app-only-authentication"></a>Java (アプリ専用認証)

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

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

### <a name="rest-app-only-authentication"></a>REST (アプリ専用認証)

#### <a name="rest-request"></a>REST 要求

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

#### <a name="rest-response"></a>REST 応答

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a>アプリ + ユーザー認証

これまで、[リソース所有者のパスワード資格情報付与](https://tools.ietf.org/html/rfc6749#section-4.3)は、パートナーセンター REST API、.net Api、Java api、または PowerShell モジュールで使用するためのアクセストークンを要求するために使用されています。 ここでは、クライアント識別子とユーザー資格情報を使用して Azure Active Directory からアクセストークンを要求します。 パートナーセンターでは、アプリ + ユーザー認証を使用する場合に multi-factor authentication が必要になるため、このアプローチは機能しなくなります。 この要件に準拠するために、Microsoft では、multi-factor authentication を使用して、クラウドソリューションプロバイダー (CSP) パートナーとコントロールパネルベンダー (CPV) を認証するための、セキュリティで保護されたスケーラブルなフレームワークを導入しました。 このフレームワークは、セキュリティで保護されたアプリケーションモデルと呼ばれ、同意プロセスと、更新トークンを使用したアクセストークンの要求で構成されます。

### <a name="partner-consent"></a>パートナーの同意

パートナーの同意プロセスは、パートナーが multi-factor authentication を使用して認証を行い、アプリケーションに同意する対話型プロセスです。更新トークンは、Azure Key Vault などのセキュリティで保護されたリポジトリに格納されます。 このプロセスには、統合のために専用のアカウントを使用することをお勧めします。

> [!IMPORTANT]  
> パートナーの同意プロセスで使用されるサービスアカウントに対して、適切な multi-factor authentication ソリューションを有効にする必要があります。 そうでない場合、結果の更新トークンはセキュリティ要件に準拠しません。

### <a name="samples-for-app--user-authentication"></a>アプリ + ユーザー認証のサンプル

パートナーの同意プロセスは、さまざまな方法で実行できます。 パートナーが必要な各操作の実行方法を理解できるように、次のサンプルを開発しました。 これらはサンプルのみであることに注意してください。 環境に適切なソリューションを実装する場合は、コーディング標準とセキュリティポリシーに準拠するソリューションを開発することが重要です。

### <a name="net-appuser-authentication"></a>.NET (アプリ + ユーザー認証)

[パートナーの同意](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault)サンプルプロジェクトでは、ASP.NET を使用して開発された web サイトを利用して同意を取得し、更新トークンを要求して、Azure Key Vault に安全に保存する方法を示します。 このサンプルに必要な前提条件を作成するには、次の手順を実行します。

1. Azure 管理ポータルまたは次の PowerShell コマンドを使用して、Azure Key Vault のインスタンスを作成します。 コマンドを実行する前に、パラメーター値が適宜変更されていることを確認してください。 コンテナー名は一意である必要があります。

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    のインスタンスの作成に関するヘルプが必要な場合は Azure Key Vault 「クイックスタート: Azure portal またはクイック Azure Key Vault スタート[を使用した Azure Key Vault からのシークレットの設定と取得](https://docs.microsoft.com/azure/key-vault/quick-create-portal)」を参照してください。 Azure Key Vault のインスタンスを作成し、シークレットを設定および取得する手順については、「 [PowerShell を使用](https://docs.microsoft.com/azure/key-vault/quick-create-powershell)したシークレットの設定と取得」を参照してください。

2. Azure 管理ポータルまたは次のコマンドを使用して、Azure AD アプリケーションとキーを作成します。

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    アプリケーション識別子とシークレット値は、次の手順で使用されるため、メモしておいてください。

3. Microsoft Azure 管理ポータルまたは次のコマンドを使用して、新しく作成した Azure AD アプリケーションにシークレットの読み取りアクセス許可を付与します。

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. パートナーセンター用に構成された Azure AD アプリケーションを作成します。 この手順を完了するには、次の操作を実行します。

    - パートナーセンターのダッシュボードの[アプリ管理](https://partner.microsoft.com/pcv/apiintegration/appmanagement)機能を参照します。
    - 新しい Azure AD アプリケーションを作成するには、[*新しい web アプリの追加*] をクリックします。

    *アプリ id*、* アカウント id * *、*キー*値は、次の手順で使用されるため、必ず文書化してください。

5. Visual Studio または次のコマンドを使用して、 [DotNet](https://github.com/Microsoft/Partner-Center-DotNet-Samples)リポジトリを複製します。

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. `Partner-Center-DotNet-Samples\secure-app-model\keyvault` ディレクトリにある*Partnerconsent*プロジェクトを開きます。
7. Web.config で検出されたアプリケーション設定を設定し[ます。](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)

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
    > アプリケーションシークレットなどの機密情報は、構成ファイルに格納しないでください。 これはサンプルアプリケーションであるため、ここで実行しました。 実稼働アプリケーションでは、証明書ベースの認証を使用することを強くお勧めします。 詳細については、「[アプリケーション認証用の証明書の資格情報](https://docs.microsoft.com/azure/active-directory/develop/active-directory-certificate-credentials)」を参照してください。

8. このサンプルプロジェクトを実行すると、認証を求めるメッセージが表示されます。 が正常に認証されると、Azure AD からアクセストークンが要求されます。 Azure AD から返される情報には、Azure Key Vault の構成済みインスタンスに格納される更新トークンが含まれています。  

### <a name="java-appuser-authentication"></a>Java (アプリ + ユーザー認証)

[パートナーの同意](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault)サンプルプロジェクトでは、JSP を使用して開発された web サイトを利用して、同意の取得、更新トークンの要求、および Azure Key Vault での secure store を行う方法を示します。 次の手順を実行して、このサンプルに必要な前提条件を作成します。

1. Azure 管理ポータルまたは次の PowerShell コマンドを使用して、Azure Key Vault のインスタンスを作成します。 コマンドを実行する前に、パラメーター値が適宜変更されていることを確認してください。 コンテナー名は一意である必要があります。

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    のインスタンスの作成に関するヘルプが必要な場合は Azure Key Vault 「[クイックスタート: Azure portal](https://docs.microsoft.com/azure/key-vault/quick-create-portal)またはクイックスタートを使用した Azure Key Vault シークレットの設定と取得」を参照してください。 Azure Key Vault のインスタンスを作成し、シークレットを設定して取得する方法に関するステップバイステップの指示については、PowerShell を使用した[Azure Key Vault から](https://docs.microsoft.com/azure/key-vault/quick-create-powershell)のシークレットの設定と取得

2. Azure 管理ポータルまたは次のコマンドを使用して、Azure AD アプリケーションとキーを作成します。

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    アプリケーション識別子とシークレット値は、次の手順で使用されるため、必ずドキュメントに記載してください。

3. Microsoft Azure 管理ポータルまたは次のコマンドを使用して、新しく作成した Azure AD アプリケーションにシークレットの読み取りアクセス許可を付与します。

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. パートナーセンター用に構成された Azure AD アプリケーションを作成します。 この手順を完了するには、次の手順を検査します。

    - パートナーセンターのダッシュボードの[アプリ管理](https://partner.microsoft.com/pcv/apiintegration/appmanagement)機能を参照します。
    - 新しい Azure AD アプリケーションを作成するには、[*新しい web アプリの追加*] をクリックします。

    *アプリ id*、* アカウント id * *、*キー*値は、次の手順で使用されるため、必ず文書化してください。

5. 次のコマンドを使用して、[パートナーセンターのサンプル](https://github.com/Microsoft/Partner-Center-Java-Samples)リポジトリを複製します。

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. `Partner-Center-Java-Samples\secure-app-model\keyvault` ディレクトリにある*Partnerconsent*プロジェクトを開きます。
7. Web .xml ファイルで検出されたアプリケーション設定を設定し[ます。](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml)

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
    > アプリケーションシークレットなどの機密情報は、構成ファイルに格納しないでください。 これはサンプルアプリケーションであるため、ここで実行しました。 実稼働アプリケーションでは、証明書ベースの認証を使用することを強くお勧めします。 詳細については、「 [Key Vault 証明書認証](https://github.com/Azure-Samples/key-vault-java-certificate-authentication)」を参照してください。

8. このサンプルプロジェクトを実行すると、認証を求めるメッセージが表示されます。 が正常に認証されると、Azure AD からアクセストークンが要求されます。 Azure AD から返される情報には、Azure Key Vault の構成済みインスタンスに格納される更新トークンが含まれています。  

## <a name="cloud-solution-provider-authentication"></a>クラウドソリューションプロバイダーの認証

クラウドソリューションプロバイダーパートナーは、[パートナーの同意](#partner-consent)プロセスを通じて取得した更新トークンを使用できます。

### <a name="samples-for-cloud-solution-provider-authentication"></a>クラウドソリューションプロバイダー認証のサンプル

パートナーが必要な各操作の実行方法を理解できるように、次のサンプルを開発しました。 これらはサンプルのみであることに注意してください。 環境に適切なソリューションを実装する場合は、コーディング標準とセキュリティポリシーに準拠するソリューションを開発することが重要です。

### <a name="net-csp-authentication"></a>.NET (CSP 認証)

1. まだ行っていない場合は、パートナーの[同意プロセス](#partner-consent)を実行します。
2. Visual Studio または次のコマンドを使用して、 [DotNet](https://github.com/Microsoft/Partner-Center-DotNet-Samples)リポジトリを複製します。

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. `Partner-Center-DotNet-Samples\secure-app-model\keyvault` ディレクトリにある `CSPApplication` プロジェクトを開きます。
4. [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config)ファイルで検出されたアプリケーション設定を更新します。

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

5. [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs)ファイルで見つかった**Partnerid**変数と**CustomerId**変数に適切な値を設定します。

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. このサンプルプロジェクトを実行すると、パートナーの同意プロセスで取得した更新トークンが取得されます。 次に、パートナーの代理としてパートナーセンター SDK と対話するアクセストークンを要求します。 最後に、指定された顧客に代わって Microsoft Graph と対話するアクセストークンを要求します。

### <a name="java-csp-authentication"></a>Java (CSP 認証)

1. まだ行っていない場合は、パートナーの[同意プロセス](#partner-consent)を実行します。
2. Visual Studio または次のコマンドを使用して、[パートナーセンターの Java サンプル](https://github.com/Microsoft/Partner-Center-Java-Samples)リポジトリを複製します。

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. `Partner-Center-Java-Samples\secure-app-model\keyvault` ディレクトリにある `cspsample` プロジェクトを開きます。
4. [アプリケーションのプロパティ](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties)ファイルで検出されたアプリケーション設定を更新します。

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. このサンプルプロジェクトを実行すると、パートナーの同意プロセスで取得した更新トークンが取得されます。 次に、パートナーの代理としてパートナーセンター SDK と対話するアクセストークンを要求します。
6. 省略可能- *RunAzureTask*および*rungraphtask*関数の呼び出しは、顧客に代わって Azure Resource Manager および Microsoft Graph と対話する方法を確認する場合に使用します。

## <a name="control-panel-provider-authentication"></a>コントロールパネルプロバイダーの認証

コントロールパネルのベンダーは、[パートナーの同意](#partner-consent)プロセスの実行をサポートする各パートナーを持っている必要があります。 この処理が完了したら、そのプロセスを通じて取得された更新トークンを使用して、パートナーセンター REST API と .NET API にアクセスします。

### <a name="samples-for-cloud-panel-provider-authentication"></a>Cloud Panel プロバイダー認証のサンプル

コントロールパネルのベンダーが必要な各操作を実行する方法を理解するために、次のサンプルを開発しました。 これらはサンプルのみであることに注意してください。 環境に適切なソリューションを実装する場合は、コーディング標準とセキュリティポリシーに準拠するソリューションを開発することが重要です。

### <a name="net-cpv-authentication"></a>.NET (CPV 認証)

1. 適切な同意を得るために、クラウドソリューションプロバイダーパートナー向けのプロセスを開発してデプロイします。 詳細と例については、[パートナーの同意](#partner-consent)を参照してください。

    > [!IMPORTANT]  
    > クラウドソリューションプロバイダーパートナーからのユーザー資格情報を格納することはできません。 パートナーの同意プロセスを通じて取得した更新トークンは、Microsoft API と対話するためのアクセストークンを要求するために保存して使用する必要があります。

2. Visual Studio または次のコマンドを使用して、 [DotNet](https://github.com/Microsoft/Partner-Center-DotNet-Samples)リポジトリを複製します。

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. `Partner-Center-DotNet-Samples\secure-app-model\keyvault` ディレクトリにある `CPVApplication` プロジェクトを開きます。
4. [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config)ファイルで検出されたアプリケーション設定を更新します。

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

5. [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs)ファイルで見つかった**Partnerid**変数と**CustomerId**変数に適切な値を設定します。

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. このサンプルプロジェクトを実行すると、指定したパートナーの更新トークンが取得されます。 次に、パートナーの代理としてパートナーセンターと Azure AD グラフにアクセスするためのアクセストークンを要求します。 次に実行されるタスクは、顧客テナントへのアクセス許可付与の削除と作成です。 コントロールパネルのベンダーと顧客の間にリレーションシップがないため、これらのアクセス許可は、パートナーセンター API を使用して追加する必要があります。 この方法を次の例に示します。

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

これらのアクセス許可が確立されると、サンプルは顧客の代わりに Azure AD グラフを使用して操作を実行します。

### <a name="java-cpv-authentication"></a>Java (CPV 認証)

1. 適切な同意を得るために、クラウドソリューションプロバイダーパートナー向けのプロセスを開発してデプロイします。 詳細と例については、[パートナーの同意](#partner-consent)を参照してください。

    > [!IMPORTANT]  
    > クラウドソリューションプロバイダーパートナーからのユーザー資格情報を格納することはできません。 パートナーの同意プロセスを通じて取得した更新トークンは、Microsoft API と対話するためのアクセストークンを要求するために保存して使用する必要があります。

2. 次のコマンドを使用して、[パートナーセンターのサンプル](https://github.com/Microsoft/Partner-Center-Java-Samples)リポジトリを複製します。

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. `Partner-Center-Java-Samples\secure-app-model\keyvault` ディレクトリにある `cpvsample` プロジェクトを開きます。
4. [アプリケーションのプロパティ](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties)ファイルで検出されたアプリケーション設定を更新します。

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

    `partnercenter.displayName` の値は、marketplace アプリケーションの表示名にする必要があります。

5. [プログラムの java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java)ファイルで見つかった**Partnerid**変数と**customerId**変数に適切な値を設定します。

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. このサンプルプロジェクトを実行すると、指定したパートナーの更新トークンが取得されます。 次に、パートナーの代理としてパートナーセンターにアクセスするためのアクセストークンを要求します。 次に実行されるタスクは、顧客テナントへのアクセス許可付与の削除と作成です。 コントロールパネルのベンダーと顧客の間にリレーションシップがないため、これらのアクセス許可は、パートナーセンター API を使用して追加する必要があります。 この方法を次の例に示します。

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

*RunAzureTask*および*rungraphtask*関数の呼び出しのコメントを解除して、顧客の代理として Azure Resource Manager および Microsoft Graph と対話する方法を確認します。
