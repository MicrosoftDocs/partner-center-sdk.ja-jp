---
title: パートナー センター Webhook
description: Webhook を使用すると、パートナーはリソース変更イベントに登録できます。
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 1ff3631ed70b197a781d2ca30d71eb8fbf211509
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097331"
---
# <a name="partner-center-webhooks"></a>パートナー センター Webhook

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーセンターの Webhook Api を使用すると、パートナーはリソース変更イベントに登録できます。 これらのイベントは、パートナーの登録済み URL に HTTP 投稿の形式で配信されます。 パートナーセンターからイベントを受信するために、パートナーはパートナーセンターがリソース変更イベントを投稿できるコールバックをホストします。 イベントはデジタル署名されるので、パートナーはパートナーセンターから送信されたことを確認できます。

パートナーは、次の例のように、パートナーセンターでサポートされている Webhook イベントから選択できます。

- **テスト イベント ("test-created")**

    このイベントを使用すると、テストイベントを要求し、その進行状況を追跡することによって、登録を自己オンボードしてテストできます。 イベントを配信しようとしているときに、Microsoft から受信されているエラーメッセージを確認できます。 この制限は、"テスト作成" イベントにのみ適用されます。 7日を経過したデータは削除されます。

- **サブスクリプション更新イベント ("subscription-updated")**

    このイベントは、サブスクリプションが変化したときに発生します。 これらのイベントは、パートナー センター API を通じて変更が行われた場合に加えて、内部変更が行われた場合にも生成されます。

    >[!NOTE]
    >サブスクリプションが変更されてからサブスクリプションの更新イベントがトリガーされるまでに、最大48時間の遅延が発生します。

- **しきい値超過イベント ("usagerecords-thresholdExceeded")**

    いずれかの顧客による Microsoft Azure の使用量が、使用量の支出予算 (しきい値) を超えると、このイベントが発生します。 詳細については、「[顧客の Azure 支出予算を設定する](https://docs.microsoft.com/partner-center/set-an-azure-spending-budget-for-your-customers)」を参照してください。

- **紹介作成イベント ("紹介-作成済み")**

    このイベントは、参照が作成されるときに発生します。

- **紹介更新イベント ("紹介-更新")**

    このイベントは、参照が更新されたときに発生します。

- **請求書の準備完了イベント ("請求書の準備完了")**

    このイベントは、新しい請求書の準備が整ったときに発生します。

将来の Webhook イベントは、パートナーが制御していないシステムで変更されるリソースに対して追加されます。また、これらのイベントを可能な限り "リアルタイム" の近くに取得するために更新が行われます。 イベントがビジネスに付加されるパートナーからのフィードバックは、追加する新しいイベントを決定する際に役立ちます。

パートナーセンターでサポートされている Webhook イベントの完全な一覧については、「[パートナーセンターの webhook イベント](partner-center-webhook-events.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

## <a name="receiving-events-from-partner-center"></a>パートナーセンターからのイベントの受信

パートナーセンターからイベントを受信するには、パブリックにアクセス可能なエンドポイントを公開する必要があります。 このエンドポイントは公開されているため、通信がパートナーセンターからのものであることを検証する必要があります。 受信したすべての Webhook イベントは、Microsoft ルートにチェーンされている証明書を使用してデジタル署名されます。 イベントの署名に使用される証明書へのリンクも提供されます。 これにより、サービスを再デプロイまたは再構成しなくても証明書を更新できます。 パートナーセンターでは、イベントの配信が10回試行されます。 10回試行してもイベントが配信されない場合は、オフラインキューに移動され、配信時にそれ以上の試行は行われません。

次のサンプルは、パートナーセンターから投稿されたイベントを示しています。

```http
POST /webhooks/callback
Content-Type: application/json
Authorization: Signature VOhcjRqA4f7u/4R29ohEzwRZibZdzfgG5/w4fHUnu8FHauBEVch8m2+5OgjLZRL33CIQpmqr2t0FsGF0UdmCR2OdY7rrAh/6QUW+u+jRUCV1s62M76jbVpTTGShmrANxnl8gz4LsbY260LAsDHufd6ab4oejerx1Ey9sFC+xwVTa+J4qGgeyIepeu4YCM0oB2RFS9rRB2F1s1OeAAPEhG7olp8B00Jss3PQrpLGOoAr5+fnQp8GOK8IdKF1/abUIyyvHxEjL76l7DVQN58pIJg4YC+pLs8pi6sTKvOdSVyCnjf+uYQWwmmWujSHfyU37j2Fzz16PJyWH41K8ZXJJkw==
X-MS-Certificate-Url: https://3psostorageacct.blob.core.windows.net/cert/pcnotifications-dispatch.microsoft.com.cer
X-MS-Signature-Algorithm: rsa-sha256
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 195

{
    "EventName": "test-created",
    "ResourceUri": "http://localhost:16722/v1/webhooks/registration/test",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

>[!NOTE]
>Authorization ヘッダーには "Signature" のスキームがあります。 これは、コンテンツの base64 でエンコードされた署名です。

## <a name="how-to-authenticate-the-callback"></a>コールバックを認証する方法

パートナーセンターから受信したコールバックイベントを認証するには、次の手順を実行します。

1. 必要なヘッダーが存在することを確認します (承認、x.509-ms-証明書 url、x.509 アルゴリズム)。

2. コンテンツに署名するために使用する証明書をダウンロードします (x-ms-certificate-url)。

3. 証明書チェーンを確認します。

4. 証明書の "組織" を確認します。

5. バッファーに UTF8 エンコードを使用してコンテンツを読み取ります。

6. RSA 暗号化プロバイダーを作成します。

7. データが、指定されたハッシュアルゴリズム (SHA256 など) で署名されたものと一致していることを確認します。

8. 検証が成功した場合は、メッセージを処理します。

> [!NOTE]
> 既定では、署名トークンは Authorization ヘッダーで送信されます。 登録で**Signaturetokentomssignatureheader**を true に設定すると、代わりに、署名トークンが x.509 署名ヘッダーで送信されます。

## <a name="event-model"></a>イベントモデル

次の表では、パートナーセンターイベントのプロパティについて説明します。

### <a name="properties"></a>Properties

| 名前                      | 説明                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | イベントの名前です。 {Resource}-{action} の形式で。 たとえば、"テスト作成" などです。  |
| **ResourceUri**           | 変更されたリソースの URI。                                                 |
| **ResourceName**          | 変更されたリソースの名前。                                                |
| **AuditUrl**              | 省略可能。 監査レコードの URI。                                                |
| **ResourceChangeUtcDate** | リソースの変更が発生した日時 (UTC 形式)。                  |

### <a name="sample"></a>サンプル

次のサンプルは、パートナーセンターイベントの構造を示しています。

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a>Webhook Api

### <a name="authentication"></a>認証

Webhook Api のすべての呼び出しは、Authorization ヘッダーのベアラートークンを使用して認証されます。 アクセスするアクセストークンを取得 https://api.partnercenter.microsoft.com します。 このトークンは、パートナーセンター Api の残りの部分にアクセスするために使用されるトークンと同じです。

### <a name="get-a-list-of-events"></a>イベントの一覧を取得する

Webhook Api で現在サポートされているイベントの一覧を返します。

### <a name="resource-url"></a>リソース URL

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a>要求の例

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200
Status: 200
Content-Length: 183
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c0bcf3a3-46e9-48fd-8e05-f674b8fd5d66
MS-RequestId: 79419bbb-06ee-48da-8221-e09480537dfc
X-Locale: en-US

[ "subscription-updated", "test-created", "usagerecords-thresholdExceeded" ]
```

### <a name="register-to-receive-events"></a>登録してイベントを受信する

指定されたイベントを受信するようにテナントを登録します。

#### <a name="resource-url"></a>リソース URL

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>要求の例

```http
POST /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0e.....
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 219

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="view-a-registration"></a>登録の表示

テナントの Webhook イベント登録を返します。

#### <a name="resource-url"></a>リソース URL

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>要求の例

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200
Status: 200
Content-Length: 341
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c3b88ab0-b7bc-48d6-8c55-4ae6200f490a
MS-RequestId: ca30367d-4b24-4516-af08-74bba6dc6657
X-Locale: en-US

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="update-an-event-registration"></a>イベント登録を更新する

既存のイベント登録を更新します。

#### <a name="resource-url"></a>リソース URL

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>要求の例

```http
PUT /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOR...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 258

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="send-a-test-event-to-validate-your-registration"></a>テストイベントを送信して登録を検証する

Webhook 登録を検証するテストイベントを生成します。 このテストは、パートナーセンターからイベントを受信できることを検証することを目的としています。 これらのイベントのデータは、最初のイベントが作成されてから7日後に削除されます。 検証イベントを送信する前に、登録 API を使用して "テスト作成" イベントに登録する必要があります。

>[!NOTE]
>検証イベントを投稿する場合、1分あたり2要求のスロットル制限があります。

#### <a name="resource-url"></a>リソース URL

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a>要求の例

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200
Status: 200
Content-Length: 181
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 04af2aea-d413-42db-824e-f328001484d1
MS-RequestId: 2f498d5a-a6ab-468f-98d8-93c96da09051
X-Locale: en-US

{ "correlationId": "04af2aea-d413-42db-824e-f328001484d1" }
```

### <a name="verify-that-the-event-was-delivered"></a>イベントが配信されたことを確認する

検証イベントの現在の状態を返します。 この確認は、イベント配信の問題のトラブルシューティングに役立ちます。 応答には、イベントを配信するために行われた各試行の結果が含まれます。

#### <a name="resource-url"></a>リソース URL

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a>要求の例

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200
Status: 200
Content-Length: 469
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 497e0a23-9498-4d6c-bd6a-bc4d6d0054e7
MS-RequestId: 0843bdb2-113a-4926-a51c-284aa01d722e
X-Locale: en-US

{
    "correlationId": "04af2aea-d413-42db-824e-f328001484d1",
    "partnerId": "00234d9d-8c2d-4ff5-8c18-39f8afc6f7f3",
    "status": "completed",
    "callbackUrl": "{{YourCallbackUrl}}",
    "results": [{
        "responseCode": "OK",
        "responseMessage": "",
        "systemError": false,
        "dateTimeUtc": "2017-12-08T21:39:48.2386997"
    }]
}
```

## <a name="example-for-signature-validation"></a>署名の検証の例

### <a name="sample-callback-controller-signature-aspnet"></a>コールバックコントローラー署名のサンプル (ASP.NET)

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a>署名の検証

次の例では、Webhook イベントからコールバックを受信しているコントローラーに Authorization 属性を追加する方法を示します。

``` csharp
namespace Webhooks.Security
{
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Security.Cryptography;
    using System.Security.Cryptography.X509Certificates;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Web.Http;
    using System.Web.Http.Controllers;
    using Microsoft.Partner.Logging;

    /// <summary>
    /// Signature based Authorization
    /// </summary>
    public class AuthorizeSignatureAttribute : AuthorizeAttribute
    {
        private const string MsSignatureHeader = "x-ms-signature";
        private const string CertificateUrlHeader = "x-ms-certificate-url";
        private const string SignatureAlgorithmHeader = "x-ms-signature-algorithm";
        private const string MicrosoftCorporationIssuer = "O=Microsoft Corporation";
        private const string SignatureScheme = "Signature";

        /// <inheritdoc/>
        public override async Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            ValidateAuthorizationHeaders(actionContext.Request);

            await VerifySignature(actionContext.Request);
        }

        private static async Task<string> GetContentAsync(HttpRequestMessage request)
        {
            // By default the stream can only be read once and we need to read it here so that we can hash the body to validate the signature from microsoft.
            // Load into a buffer, so that the stream can be accessed here and in the api when it binds the content to the expected model type.
            await request.Content.LoadIntoBufferAsync();

            var s = await request.Content.ReadAsStreamAsync();
            var reader = new StreamReader(s);
            var body = await reader.ReadToEndAsync();

            // set the stream position back to the beginning
            if (s.CanSeek)
            {
                s.Seek(0, SeekOrigin.Begin);
            }

            return body;
        }

        private static void ValidateAuthorizationHeaders(HttpRequestMessage request)
        {
            var authHeader = request.Headers.Authorization;
            if (string.IsNullOrWhiteSpace(authHeader?.Parameter) && string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, MsSignatureHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Authorization header missing."));
            }

            var signatureHeaderValue = GetHeaderValue(request.Headers, MsSignatureHeader);
            if (authHeader != null
                && !string.Equals(authHeader.Scheme, SignatureScheme, StringComparison.OrdinalIgnoreCase)
                && !string.IsNullOrWhiteSpace(signatureHeaderValue)
                && !signatureHeaderValue.StartsWith(SignatureScheme, StringComparison.OrdinalIgnoreCase))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Authorization scheme needs to be '{SignatureScheme}'."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, CertificateUrlHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {CertificateUrlHeader} missing."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, SignatureAlgorithmHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {SignatureAlgorithmHeader} missing."));
            }
        }

        private static string GetHeaderValue(HttpHeaders headers, string key)
        {
            headers.TryGetValues(key, out var headerValues);

            return headerValues?.FirstOrDefault();
        }

        private static async Task VerifySignature(HttpRequestMessage request)
        {
            // Get signature value from either authorization header or x-ms-signature header.
            var base64Signature = request.Headers.Authorization?.Parameter ?? GetHeaderValue(request.Headers, MsSignatureHeader).Split(' ')[1];
            var signatureAlgorithm = GetHeaderValue(request.Headers, SignatureAlgorithmHeader);
            var certificateUrl = GetHeaderValue(request.Headers, CertificateUrlHeader);
            var certificate = await GetCertificate(certificateUrl);
            var content = await GetContentAsync(request);
            var alg = signatureAlgorithm.Split('-'); // for example RSA-SHA1
            var isValid = false;

            var logger = GetLoggerIfAvailable(request);

            // Validate the certificate
            VerifyCertificate(certificate, request, logger);

            if (alg.Length == 2 && alg[0].Equals("RSA", StringComparison.OrdinalIgnoreCase))
            {
                var signature = Convert.FromBase64String(base64Signature);
                var csp = (RSACryptoServiceProvider)certificate.PublicKey.Key;

                var encoding = new UTF8Encoding();
                var data = encoding.GetBytes(content);

                var hashAlgorithm = alg[1].ToUpper();

                isValid = csp.VerifyData(data, CryptoConfig.MapNameToOID(hashAlgorithm), signature);
            }

            if (!isValid)
            {
                // log that we were not able to validate the signature
                logger?.TrackTrace(
                    "Failed to validate signature for webhook callback",
                    new Dictionary<string, string> { { "base64Signature", base64Signature }, { "certificateUrl", certificateUrl }, { "signatureAlgorithm", signatureAlgorithm }, { "content", content } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Signature verification failed"));
            }
        }

        private static ILogger GetLoggerIfAvailable(HttpRequestMessage request)
        {
            return request.GetDependencyScope().GetService(typeof(ILogger)) as ILogger;
        }

        private static async Task<X509Certificate2> GetCertificate(string certificateUrl)
        {
            byte[] certBytes;
            using (var webClient = new WebClient())
            {
                certBytes = await webClient.DownloadDataTaskAsync(certificateUrl);
            }

            return new X509Certificate2(certBytes);
        }

        private static void VerifyCertificate(X509Certificate2 certificate, HttpRequestMessage request, ILogger logger)
        {
            if (!certificate.Verify())
            {
                logger?.TrackTrace("Failed to verify certificate for webhook callback.", new Dictionary<string, string> { { "Subject", certificate.Subject }, { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Certificate verification failed."));
            }

            if (!certificate.Issuer.Contains(MicrosoftCorporationIssuer))
            {
                logger?.TrackTrace($"Certificate not issued by {MicrosoftCorporationIssuer}.", new Dictionary<string, string> { { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Certificate not issued by {MicrosoftCorporationIssuer}."));
            }
        }
    }
}
```
