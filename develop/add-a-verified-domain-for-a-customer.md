---
title: 顧客の確認済みドメインを追加する
description: パートナーセンターで、お客様の承認済みドメインの一覧に検証済みドメインを追加します。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d1503506d520671834c6290cddd487fc471090c2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095421"
---
# <a name="add-a-verified-domain-for-a-customer"></a>顧客の確認済みドメインを追加する

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

検証済みドメインを既存の顧客の承認済みドメインの一覧に追加する方法。

## <a name="prerequisites"></a>必須コンポーネント

- ドメインレジストラーであるパートナーである必要があります。

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="adding-a-verified-domain"></a>検証済みドメインの追加

ドメインレジストラーのパートナーである場合は、API を使用して、 `verifieddomain` 既存の顧客のドメインの一覧に新しい[ドメイン](#domain)リソースを投稿できます。 これを行うには、顧客の Tenantid を使用して顧客を識別します。 VerifiedDomainName プロパティの値を指定します。 要求の中に、必要な Name、機能、AuthenticationType、Status、および VerificationMethod の各プロパティを指定して[ドメイン](#domain)リソースを渡します。 新しい[ドメイン](#domain)がフェデレーションドメインであることを指定するには、[ドメイン](#domain)リソースの AuthenticationType プロパティをに設定 `Federated` し、要求に[microsoft.online.administration.domainfederationsettings](#domain-federation-settings)リソースを含めます。 メソッドが成功した場合、応答には新しい検証済みドメインの[ドメイン](#domain)リソースが含まれます。

### <a name="custom-verified-domains"></a>カスタム検証済みドメイン

**Onmicrosoft.com**に登録されていないドメインであるカスタム確認済みドメインを追加する場合は、ドメインを追加する顧客の一意の ID 値に、[ユーザーの immutableid](user-resources.md#customeruser)プロパティを設定する必要があります。 この一意識別子は、検証プロセス中にドメインを検証するときに必要です。 顧客のユーザーアカウントの詳細については、「[顧客のユーザーアカウントを作成](create-user-accounts-for-a-customer.md)する」を参照してください。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法 | 要求 URI                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

次のクエリパラメーターを使用して、確認済みドメインを追加する顧客を指定します。

| 名前                   | Type     | 必須 | 説明                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| 顧客 Tenantid | guid | Y        | 値は、顧客を指定できるようにする GUID 形式の顧客**tenantid**です。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

次の表では、要求本文に必要なプロパティについて説明します。

| 名前                                                  | Type   | 必須                                      | 説明                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | string | はい                                           | 検証済みのドメイン名。 |
| [ドメイン](#domain)                                     | object | はい                                           | ドメイン情報が含まれています。 |
| [Microsoft.online.administration.domainfederationsettings](#domain-federation-settings) | object | はい (AuthenticationType がの場合 = `Federated` )     | ドメインがドメインではなくドメインである場合に使用されるドメインフェデレーション設定 `Federated` `Managed` 。 |

### <a name="domain"></a>ドメイン

次の表では、要求本文の必須のドメインプロパティと省略可能な**ドメイン**プロパティについて説明します。

| 名前               | Type                                     | 必須 | 説明                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType                                    | string           | はい      | ドメインが `Managed` ドメインかドメインかを定義 `Federated` します。 サポートされる値: `Managed` 、 `Federated` 。|
| 機能                                            | string           | はい      | ドメインの機能を指定します。 例: `Email`                  |
| IsDefault                                             | null 許容のブール値 | いいえ       | ドメインがテナントの既定のドメインかどうかを示します。 サポートされる値: `True` 、 `False` 、 `Null` 。        |
| IsInitial                                             | null 許容のブール値 | いいえ       | ドメインが初期ドメインであるかどうかを示します。 サポートされる値: `True` 、 `False` 、 `Null` 。                       |
| 名前                                                  | string           | はい      | ドメイン名。                                                          |
| RootDomain                                            | 文字列           | いいえ       | ルートドメインの名前。                                              |
| 状態                                                | string           | はい      | ドメインの状態。 例: `Verified` サポートされる値: `Unverified` 、 `Verified` 、 `PendingDeletion` 。                               |
| VerificationMethod                                    | string           | はい      | ドメインの確認方法の種類。 サポートされる値: `None` 、 `DnsRecord` 、 `Email` 。                                    |

### <a name="domain-federation-settings"></a>ドメインのフェデレーション設定

次の表では、要求本文の必須プロパティとオプションの**microsoft.online.administration.domainfederationsettings**プロパティについて説明します。

| 名前   | Type   | 必須 | 説明                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | 文字列           | いいえ      | リッチクライアントによって使用されるログオン URI。 このプロパティは、パートナーの STS 認証 URL です。 |
| DefaultInteractiveAuthenticationMethod | 文字列           | いいえ      | アプリケーションがユーザーに対話型ログインを要求するときに使用する、既定の認証方法を示します。 |
| FederationBrandName                    | 文字列           | いいえ      | フェデレーションブランド名。        |
| IssuerUri                              | string           | はい     | 証明書の発行者の名前。                        |
| LogOffUri                              | string           | はい     | ログオフ URI。 このプロパティでは、フェデレーションドメインのサインアウト URI について説明します。        |
| MetadataExchangeUri                    | 文字列           | いいえ      | リッチクライアントアプリケーションからの認証に使用されるメタデータ交換エンドポイントを指定する URL。 |
| NextSigningCertificate                 | 文字列           | いいえ      | ADFS V2 STS によって要求に署名するために将来使用される証明書。 このプロパティは、証明書の base64 でエンコードされた表現です。 |
| OpenIdConnectDiscoveryEndpoint         | 文字列           | いいえ      | フェデレーション IDP STS の OpenID Connect 検出エンドポイント。 |
| PassiveLogOnUri                        | string           | はい     | 古いパッシブクライアントによって使用されるログオン URI。 このプロパティは、フェデレーションサインイン要求を送信するアドレスです。 |
| PreferredAuthenticationProtocol        | string           | はい     | 認証トークンの形式。 例: `WsFed` サポートされる値: `WsFed` 、`Samlp` |
| PromptLoginBehavior                    | string           | はい     | プロンプトのログイン動作の種類です。  例: `TranslateToFreshPasswordAuth` サポートされる値: `TranslateToFreshPasswordAuth` 、 `NativeSupport` 、`Disabled` |
| SigningCertificate                     | string           | はい     | ADFS V2 STS が要求に署名するために現在使用している証明書。 このプロパティは、証明書の base64 でエンコードされた表現です。 |
| SigningCertificateUpdateStatus         | 文字列           | いいえ      | 署名証明書の更新状態を示します。 |
| SigningCertificateUpdateStatus         | null 許容のブール値 | いいえ      | IDP STS が MFA をサポートするかどうかを示します。 サポートされる値: `True` 、 `False` 、 `Null` 。|

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

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

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
