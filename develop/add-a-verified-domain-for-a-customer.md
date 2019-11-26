---
title: 顧客の確認済みドメインを追加する
description: パートナーセンターで、お客様の承認済みドメインの一覧に検証済みドメインを追加します。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: f5abd926389c1c81a178fe5cd2476929070657f6
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486222"
---
# <a name="add-a-verified-domain-for-a-customer"></a>顧客の確認済みドメインを追加する

適用対象:

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

検証済みドメインを既存の顧客の承認済みドメインの一覧に追加する方法。

## <a name="prerequisites"></a>前提条件

- ドメインレジストラーであるパートナーである必要があります。
- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客 ID (顧客**tenantid**)。 顧客の ID を持っていない場合、パートナーセンターで ID を検索するには、顧客 の一覧から顧客を選択し、**アカウント** を選択して、Microsoft id を保存します。

## <a name="adding-a-verified-domain"></a>検証済みドメインの追加

ドメインレジストラーのパートナーである場合は、verifieddomain API を使用して、既存の顧客のドメインの一覧に新しい[ドメイン](#domain)リソースを投稿できます。 これを行うには、顧客の Tenantid を使用して顧客を特定し、VerifiedDomainName プロパティの値を指定します。次に、要求の中で、必要な Name、機能、AuthenticationType、Status、および VerificationMethod プロパティを使用して[ドメイン](#domain)リソースを渡します。 新しい[ドメイン](#domain)がフェデレーションドメインであることを指定するには、[ドメイン](#domain)リソースの AuthenticationType プロパティを "フェデレーション" に設定し、要求に[microsoft.online.administration.domainfederationsettings](#domain-federation-settings)リソースを含めます。 メソッドが成功した場合、応答には新しい検証済みドメインの[ドメイン](#domain)リソースが含まれます。

### <a name="custom-verified-domains"></a>カスタム検証済みドメイン

**Onmicrosoft.com**に登録されていないドメインであるカスタム確認済みドメインを追加する場合は、ドメインを追加する顧客の一意の ID 値に、[ユーザーの immutableid](user-resources.md#customeruser)プロパティを設定する必要があります。 この一意識別子は、検証プロセス中にドメインを検証するときに必要です。 顧客のユーザーアカウントの詳細については、「[顧客のユーザーアカウントを作成](create-user-accounts-for-a-customer.md)する」を参照してください。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを使用して、確認済みドメインを追加する顧客を指定します。

| 名前                   | 種類     | 必須 | 説明                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| 顧客 Tenantid | guid | Y        | 値は、顧客を指定できるようにする GUID 形式の顧客**tenantid**です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>要求本文

次の表では、要求本文に必要なプロパティについて説明します。

| 名前                                                  | 種類   | 必須                                      | 説明                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | string | 〇                                           | 検証済みのドメイン名。 |
| [Domain](#domain)                                     | オブジェクト | 〇                                           | ドメイン情報が含まれています。 |
| [Microsoft.online.administration.domainfederationsettings](#domain-federation-settings) | オブジェクト | はい (AuthenticationType が "フェデレーション" の場合)     | ドメインが "フェデレーション" ドメインで、"管理された" ドメインではない場合に使用されるドメインフェデレーション設定。 |

#### <a name="domain"></a>ドメイン

次の表では、要求本文の必須のドメインプロパティと省略可能な**ドメイン**プロパティについて説明します。

| 名前               | 種類                                     | 必須 | 説明                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType                                    | string           | 〇      | ドメインが "管理されている" ドメインであるか "フェデレーション" ドメインであるかを定義します。 サポートされる値: 管理、フェデレーション。|
| 機能                                            | string           | 〇      | ドメインの機能を指定します。 たとえば、"Email" のようにします。                  |
| IsDefault                                             | null 許容のブール値 | X       | ドメインがテナントの既定のドメインかどうかを示します。 サポートされる値: True、False、Null。        |
| IsInitial                                             | null 許容のブール値 | X       | ドメインが初期ドメインであるかどうかを示します。 サポートされる値: True、False、Null。                       |
| 名前                                                  | string           | 〇      | ドメイン名。                                                          |
| RootDomain                                            | string           | X       | ルートドメインの名前。                                              |
| 状況                                                | string           | 〇      | ドメインの状態。 たとえば、"確認済み" などです。 サポートされている値: 未確認、検証済み、PendingDeletion。                               |
| VerificationMethod                                    | string           | 〇      | ドメインの確認方法の種類。 サポートされている値: なし、DnsRecord、Email。                                    |

##### <a name="domain-federation-settings"></a>ドメインのフェデレーション設定

次の表では、要求本文の必須プロパティとオプションの**microsoft.online.administration.domainfederationsettings**プロパティについて説明します。

| 名前   | 種類   | 必須 | 説明                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | string           | X      | リッチクライアントによって使用されるログオン URI。 これは、パートナーの STS 認証 URL です。 |
| DefaultInteractiveAuthenticationMethod | string           | X      | アプリケーションがユーザーに対話型ログインを要求するときに使用する、既定の認証方法を示します。 |
| FederationBrandName                    | string           | X      | フェデレーションブランド名。        |
| IssuerUri                              | string           | 〇     | 証明書の発行者の名前。                        |
| LogOffUri                              | string           | 〇     | ログオフ URI。 フェデレーションドメインのサインアウト URI について説明します。        |
| MetadataExchangeUri                    | string           | X      | リッチクライアントアプリケーションからの認証に使用されるメタデータ交換エンドポイントを指定する URL。 |
| NextSigningCertificate                 | string           | X      | ADFS V2 STS によって要求に署名するために将来使用される証明書。 これは、証明書の base64 でエンコードされた表現です。 |
| OpenIdConnectDiscoveryEndpoint         | string           | X      | フェデレーション IDP STS の OpenID Connect 検出エンドポイント。 |
| "いいえ Velogonuri"                        | string           | 〇     | 古いパッシブクライアントによって使用されるログオン URI。 これは、フェデレーションサインイン要求を送信するためのアドレスです。 |
| PreferredAuthenticationProtocol        | string           | 〇     | 認証トークンの形式。 たとえば、"WsFed" などです。 サポートされる値: WsFed、Samlp |
| PromptLoginBehavior                    | string           | 〇     | プロンプトのログイン動作の種類です。  たとえば、"TranslateToFreshPasswordAuth" のようになります。 サポートされる値: TranslateToFreshPasswordAuth、NativeSupport、Disabled |
| SigningCertificate                     | string           | 〇     | ADFS V2 STS が要求に署名するために現在使用している証明書。 これは、証明書の base64 でエンコードされた表現です。 |
| SigningCertificateUpdateStatus         | string           | X      | 署名証明書の更新状態を示します。 |
| SigningCertificateUpdateStatus         | null 許容のブール値 | X      | IDP STS が MFA をサポートするかどうかを示します。 サポートされる値: True、False、Null。|

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
    "VerifiedDomainName": "Example.com",
    "Domain": {
        "AuthenticationType": "Federated",
        "Capability": "Email",
        "IsDefault": Null,
        "IsInitial": Null,
        "Name": "Example.com",
        "RootDomain": null,
        "Status": "Verified",
        "VerificationMethod": "None"
    },
    "DomainFederationSettings": {
        "ActiveLogOnUri": "https://sts.microsoftonline.com/FederationPassive/",
        "DefaultInteractiveAuthenticationMethod": "http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password",
        "FederationBrandName": "FederationBrandName",
        "IssuerUri": "Example.com",
        "LogOffUri": "https://sts.microsoftonline.com/FederationPassive/",
        "MetadataExchangeUri": null,
        "NextSigningCertificate": null,
        "OpenIdConnectDiscoveryEndpoint": "https://sts.contoso.com/adfs/.well-known/openid-configuration",
        "PassiveLogOnUri": "https://sts.microsoftonline.com/Trust/2005/UsernameMixed",
        "PreferredAuthenticationProtocol": "WsFed",
        "PromptLoginBehavior": "TranslateToFreshPasswordAuth",
        "SigningCertificate": <Certificate Signature goes here>,
        "SigningCertificateUpdateStatus": null,
        "SupportsMfa": true
    }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、この API は新しい検証済みドメインの[ドメイン](#domain)リソースを返します。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 201 Created
Content-Length: 206
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "authenticationType": "federated",
    "capability": "email",
    "isDefault": false,
    "isInitial": false,
    "name": "Example.com",
    "status": "verified",
    "verificationMethod": "dns_record"
}
```