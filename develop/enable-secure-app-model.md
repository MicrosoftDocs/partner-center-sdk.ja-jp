---
title: Enable secure application model
description: Secure your Partner Center and control panel apps.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 248de75fd97405a5386628ee47ae16661cdef9f8
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74490102"
---
# <a name="enabling-the-secure-application-model-framework"></a>Enabling the Secure Application Model framework

適用対象:

- パートナー センター

Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.

You can use the new model to elevate security for Partner Center API integration calls. This will help all parties (including Microsoft, CSP partners, and CPVs) to protect their infrastructure and customer data from security risks.

## <a name="scope"></a>適用範囲

This topic concerns the following actors:

- CPVs
  - A CPV is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs.
  - A CPV is not a CSP partner with direct access to the Partner Center dashboard or APIs.
- CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.

## <a name="security-requirements"></a>セキュリティ要件

For details on security requirements, see [Partner Security Requirements](https://docs.microsoft.com/partner-center/partner-security-requirements).

## <a name="secure-application-model"></a>セキュリティで保護されたアプリケーション モデル

Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs. Security attacks on these sensitive applications can lead to the compromise of customer data.

For an overview and details of the new authentication framework, download the [Secure Application Model framework](http://assetsprod.microsoft.com/secure-application-model-guide.pdf) document. This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.

## <a name="samples"></a>サンプル

The following overview documents and sample code describe how partners can implement the Secure Application Model framework:

- [CPV overview document](http://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [CSP overview document](http://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [.NET Samples](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Java Samples](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

- [REST instructions and samples](#rest)
- [PowerShell instructions and samples](#powershell)

## <a name="rest"></a>REST

To to make REST calls with the Secure Application Model framework with sample code, you must do the following:

1. [Create a web app](#create-a-web-app)
2. [Get an authorization code](#get-authorization-code)
3. [Get a refresh token](#get-refresh-token)
4. [Get an access token](#get-access-token)
5. [Make a Partner Center API call](#make-partner-center-api-calls)

> [!TIP]
> You can use the Partner Center PowerShell module to get an authorization code and a refresh token. You can choose this option in place of steps 2 and 3. For more information, see the [PowerShell section and examples](#powershell).

### <a name="create-a-web-app"></a>Create a web app

You must create and register a web app in Partner Center before making REST calls.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Create an Azure Active Directory (Azure AD) app.
3. Give delegated application permissions to the following resources, *depending on your application's requirements*. If necessary, you can add more delegated permissions for application resources.
    1. **Microsoft Partner Center** (some tenants show this as **SampleBECApp**)
    2. **Azure Management APIs** (if you are planning to call Azure APIs)
    3. **Windows Azure Active Directory**
4. Make sure that the home URL of your app is set to an endpoint where a live web app is running. This app will need to accept the [authorization code](#get-authorization-code) from the Azure AD login call. For example, in the example code in [the following section](#get-authorization-code), the web app is running at `https://localhost:44395/`.
5. Note the following information from your web app's settings in Azure AD:
    - アプリケーション ID
    - Application secret

> [!NOTE]
> It is recommended to [use a certificate as your application secret](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-certificate-credentials). However, you can also create an application key in the Azure portal. The sample code in [the following section](#get-authorization-code) uses an application key.

### <a name="get-authorization-code"></a>Get authorization code

You must get an authorization code for your web app to accept from the Azure AD login call:

1. Log in to Azure AD at the following URL: <https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile>. Be sure to log in with the user account from which you will make Partner Center API calls (such as an admin agent or sales agent account).
2. Replace **Application-Id** with your Azure AD app ID (GUID).
3. When prompted, log in with your user account with MFA configured.
4. When prompted, enter additional MFA information (phone number or email address) to verify your login.
5. After you are logged in, the browser will redirect the call to your web app endpoint with your authorization code. For example, the following sample code redirects to `https://localhost:44395/`.

#### <a name="authorization-code-call-trace"></a>Authorization code call trace

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

### <a name="get-refresh-token"></a>Get refresh token

You must then use your authorization code to get a refresh token:

1. Make a POST call to the Azure AD login endpoint `https://login.microsoftonline.com/CSPTenantID/oauth2/token` with the authorization code. For an example, see the following [sample call](#sample-refresh-call).
2. Note the refresh token that is returned.
3. Store the refresh token in Azure Key Vault. For more information, see the [Key Vault API documentation](https://docs.microsoft.com/en-us/rest/api/keyvault/).

> [!IMPORTANT]
> The refresh token must be [stored as a secret](https://docs.microsoft.com/en-us/rest/api/keyvault/setsecret/setsecret) in Key Vault.

#### <a name="sample-refresh-call"></a>Sample refresh call

Placeholder request:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

Request body:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

Placeholder response:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Response body:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a>アクセス トークンを取得する

You must obtain an access token before you can make calls to the Partner Center APIs. You must use a refresh token to obtain an access token because access token generally have a very limited lifetime (for example, less than an hour).

Placeholder request:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

Request body:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

Placeholder response:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Response body:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a>Make Partner Center API calls

You must use your access token to call the Partner Center APIs. See the following example call.

#### <a name="example-partner-center-api-call"></a>Example Partner Center API call

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

You can use the [Partner Center PowerShell module](https://www.powershellgallery.com/packages/PartnerCenter) to reduce the required infrastructure to exchange an authorization code for an access token. This method is optional for making [Partner Center REST calls](#rest).

For more information on this process, see [Secure App Model](https://docs.microsoft.com/en-us/powershell/partnercenter/secure-app-model) PowerShell documentation.

1. Install the Azure AD and Partner Center PowerShell modules.

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. Use PowerShell to add `urn:ietf:wg:oauth:2.0:oob` as a reply URL for your Azure AD application. Be sure to replace the value for the object identifier parameter with the object identifier for you Azure AD application. You can find this value in the Azure management portal.

    ```powershell
    Connect-AzureAD
    ```

    ```powershell
    Set-AzureADApplication -ObjectId 659dd68d-3414-4254-a48b-c081b5631b86 -ReplyUrls @("urn:ietf:wg:oauth:2.0:oob")
    ```

3. Use the **[New-PartnerAccessToken](https://docs.microsoft.com/powershell/module/partnercenter/new-partneraccesstoken)** command to perform the consent process and capture the required refresh token.

    ```powershell
    $credential = Get-Credential
    ```

    ```powershell
    $token = New-PartnerAccessToken -Consent -Credential $credential -Resource https://api.partnercenter.microsoft.com -ServicePrincipal
    ```

    > [!NOTE]
    > The **ServicePrincipal** parameter is used with the **New-PartnerAccessToken** command because an Azure AD app with a type of **web/API** is being used. This type of app require that a client identifier and secret be included in the access token request.

4. Copy the refresh token value.

    ```powershell
    $token.RefreshToken | clip
    ```

5. When the **Get-Credential** command is invoked, you will be prompted to enter a username and password. Enter the application identifier as teh username. Enter the application secret as the password.

6. When the **New-PartnerAccessToken** command is invoked, you will be prompted to enter credentials again. Enter the credentials for the service account that you are using. This service account should be a partner account with apppropriate permissions.

7. After the **New-PartnerAccessToken** is successfully executed, the **$token** variable now contains the response from Azure AD. Be sure to note and store the refresh token value in a secure repository, such as Azure Key Vault.
