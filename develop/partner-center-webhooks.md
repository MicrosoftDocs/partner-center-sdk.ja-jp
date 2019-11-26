---
title: Partner Center webhooks
description: Webhooks allow partners to register for resource change events.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 6bb15fc4879bb735264ab45c4a84f6581cbf094a
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488242"
---
# <a name="partner-center-webhooks"></a>Partner Center webhooks


**Applies To**

- パートナー センター   
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター   


The Partner Center Webhook APIs allow partners to register for resource change events. These events are delivered in the form of HTTP POSTs to the partner's registered URL. To receive an event from Partner Center, partners will host a callback where Partner Center can POST the resource change event. The event will be digitally signed so that the partner can verify that it was sent from Partner Center. 

Partners can select from Webhook events, like the following, that are supported by Partner Center.  

- **Test Event ("test-created")**

    This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress. You will be able to see the failure messages that are being received from Microsoft while trying to deliver the event. This will only apply to "test-created" events and data older than 7 days will be purged.

- **Subscription Updated Event ("subscription-updated")**

    このイベントは、サブスクリプションが変化したときに発生します。 これらのイベントは、パートナー センター API を通じて変更が行われた場合に加えて、内部変更が行われた場合にも生成されます。 
    
    >[!NOTE]
    >There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered. 

- **Threshold Exceeded Event ("usagerecords-thresholdExceeded")**

    いずれかの顧客による Microsoft Azure の使用量が、使用量の支出予算 (しきい値) を超えると、このイベントが発生します。 For more information, see  [Set an Azure spending budget for your customers](https://docs.microsoft.com/partner-center/set-an-azure-spending-budget-for-your-customers).

- **Referral Created Event ("referral-created")**

    This event is raised when the referral is created. 

- **Referral Updated Event ("referral-updated")**

    This event is raised when the referral is updated. 

- **Invoice Ready Event ("invoice-ready")**

    This event is raised when the new invoice is ready.


Future Webhook events will be added for resources that change in the system that the partner is not in control of, and further updates will be made to get those events as close to "real time" as possible. Feedback from Partners on which events add value to their business will be extremely useful in determing which new events to add. 

For a complete list of Webhook events supported by Partner Center, see [Partner Center webhook events](partner-center-webhook-events.md).

## <a name="prerequisites"></a>前提条件


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.   



## <a name="receiving-events-from-partner-center"></a>Receiving events from Partner Center

To receive events from Partner Center, you must expose a publicly accessible endpoint; and because this endpoint is exposed, you must validate that the communication is from Partner Center. All Webhook events that you receive are digitally signed with a certificate that chains to the Microsoft Root. A link to the certificate used to sign the event will also be provided. This will allow the certificate to be renewed without you having to re-deploy or re-configure your service. Partner Center will make 10 attempts to deliver the event. If the event is still not delivered after 10 attempts, it will me moved into an offline queue and no further attempts will be made at delivery. 

The following sample shows an event posted from Partner Center.

```http
POST /webhooks/callback
Content-Type: application/json
Authorization: Signature VOhcjRqA4f7u/4R29ohEzwRZibZdzfgG5/w4fHUnu8FHauBEVch8m2+5OgjLZRL33CIQpmqr2t0FsGF0UdmCR2OdY7rrAh/6QUW+u+jRUCV1s62M76jbVpTTGShmrANxnl8gz4LsbY260LAsDHufd6ab4oejerx1Ey9sFC+xwVTa+J4qGgeyIepeu4YCM0oB2RFS9rRB2F1s1OeAAPEhG7olp8B00Jss3PQrpLGOoAr5+fnQp8GOK8IdKF1/abUIyyvHxEjL76l7DVQN58pIJg4YC+pLs8pi6sTKvOdSVyCnjf+uYQWwmmWujSHfyU37j2Fzz16PJyWH41K8ZXJJkw==
X-MS-Certificate-Url: https://3psostorageacct.blob.core.windows.net/cert/pcnotifications.microsoft.com.cer
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
>The Authorization header has a scheme of "Signature". This is a base64 encoded signature of the content.

## <a name="how-to-authenticate-the-callback"></a>How to authenticate the callback


To authenticate the callback event received from Partner Center, do the following:

1.  Verify the required headers are present (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).
2.  Download the certificate used to sign the content (x-ms-certificate-url).
3.  Verify the Certificate Chain.
4.  Verify the "Organization" of the certificate.
5.  Read the content with UTF8 encoding into a buffer.
6.  Create an RSA Crypto Provider.
7.  Verify the data matches what was signed with the specified hash algorithm (e.g. SHA256).
8.  If the verification succeeds, process the message.

> [!NOTE]
> By default, the signature token will be sent in an Authorization header. If you set **SignatureTokenToMsSignatureHeader** to true in your registration, the signature token will be sent in the x-ms-signature header instead.

## <a name="event-model"></a>Event model


The following table describes the properties of a Partner Center event.

**[プロパティ]**

| 名前                      | 説明                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | The name of the event. In the form {resource}-{action}. For example, "test-created".  |
| **ResourceUri**           | The URI of the resource that changed.                                                 |
| **ResourceName**          | The name of the resource that changed.                                                |
| **AuditUrl**              | (省略可能)。 The URI of the Audit record.                                                |
| **ResourceChangeUtcDate** | The date and time, in UTC format, when the resource change occurred.                  |


**Sample**

The following sample shows the structure of a Partner Center event.

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```


## <a name="webhook-apis"></a>Webhook APIs   


**[認証]**   

All calls to the Webhook APIs are authenticated using the Bearer token in the Authorization Header. You must acquire an access token to access https://api.partnercenter.microsoft.com. This is the same token that is used to access the rest of the Partner Center APIs.


 
### <a name="get-a-list-of-events"></a>Get a list of events

Returns a list of the events that are currently supported by the Webhook APIs.

**Resource URL**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration/events

**Request example**   

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

**Response example**   

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



### <a name="register-to-receive-events"></a>Register to receive events      

Registers a tenant to receive the specified events.

**Resource URL**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration


**Request example**   

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

**Response example**   

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



### <a name="view-a-registration"></a>View a registration        

Returns the Webhooks event registration for a tenant.

**Resource URL**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration


**Request example**   

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

**Response example**   

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



### <a name="update-an-event-registration"></a>Update an event registration      

Updates an existing event registration. 

**Resource URL**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration


**Request example**   

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

**Response example**   

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


### <a name="send-a-test-event-to-validate-your-registration"></a>Send a test event to validate your registration   

Generates a test event to validate the Webhooks registration. This test is intended to validate that you can receive events from Partner Center. Data for these events will be deleted 7 days after the initial event is created. You must be registered for the "test-created" event, using the registration API, before sending a validation event. 

>[!NOTE]
>There is a throttle limit of 2 requests per minute when posting a validation event. 

**Resource URL**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents

**Request example**   

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

**Response example**   

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



### <a name="verify-that-the-event-was-delivered"></a>Verify that the event was delivered   

Returns the current state of the validation event. This can be helpful for trouble shooting event delivery issues. The Response contains a result for each attempt that is made to deliver the event.

**Resource URL**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}

**Request example**   

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

**Response example**     

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


## <a name="example-for-signature-validation"></a>Example for Signature Validation


**Sample Callback Controller signature (ASP.NET)**     

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

**Signature Validation**      
The following example shows how to add an Authorization Attribute to the controller that is receiving callbacks from Webhook events.

``` csharp
namespace Webhooks.Security
{
    using System;
    using System.Collections.Generic;
    using System.Diagnostics;
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
        private const string CertificateUrlHeader = "x-ms-certificate-url";
        private const string SignatureAlgorithmHeader = "x-ms-signature-algorithm";

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
            if (authHeader == null || string.IsNullOrEmpty(authHeader.Parameter))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Authorization Header missing"));
            }

            if (authHeader.Scheme != "Signature")
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Authorization Scheme needs to be 'Signature'"));
            }

            if (string.IsNullOrEmpty(GetHeaderValue(request.Headers, CertificateUrlHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {CertificateUrlHeader} missing"));
            }

            if (string.IsNullOrEmpty(GetHeaderValue(request.Headers, SignatureAlgorithmHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {SignatureAlgorithmHeader} missing"));
            }
        }

        private static string GetHeaderValue(HttpRequestHeaders headers, string key)
        {
            headers.TryGetValues(key, out IEnumerable<string> headerValues);

            return headerValues?.FirstOrDefault();
        }

        private static async Task VerifySignature(HttpRequestMessage request)
        {
            var base64Signture = request.Headers.Authorization?.Parameter;
            var signatureAlgorithm = GetHeaderValue(request.Headers, SignatureAlgorithmHeader);
            var certificateUrl = GetHeaderValue(request.Headers, CertificateUrlHeader);
            var certificate = await GetCertificate(certificateUrl);
            var content = await GetContentAsync(request);
            var alg = signatureAlgorithm.Split('-');    // e.g. RSA-SHA1
            var isValid = false;

            // Validate the certificate
            if (VerifyCertificate(certificate))
            {
                if (alg.Length == 2 && alg[0].Equals("RSA", StringComparison.OrdinalIgnoreCase))
                {
                    byte[] signature = Convert.FromBase64String(base64Signture);

                    RSACryptoServiceProvider csp = (RSACryptoServiceProvider)certificate.PublicKey.Key;

                    var encoding = new UTF8Encoding();
                    byte[] data = encoding.GetBytes(content);

                    string hashAlgorithm = alg[1].ToUpper();

                    isValid = csp.VerifyData(data, CryptoConfig.MapNameToOID(hashAlgorithm), signature);
                }

                if (!isValid)
                {
                    // log that we were not able to validate the signature
                    Trace.WriteLine($"Failed to validate signature for webhook callback. base64Signature: {base64Signture}, certificateUrl: {certificateUrl}, signatureAlgorithm: {signatureAlgorithm}");

                    var logger = GetLoggerIfAvailable(request);
                    logger?.TrackTrace("Failed to validate Signature for webhook callback", new Dictionary<string, string> { { "base64Signature", base64Signture }, { "certificateUrl", certificateUrl }, { "signatureAlgorithm", signatureAlgorithm }, { "content", content } });

                    throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Signature verification failed"));
                }
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

        private static bool VerifyCertificate(X509Certificate2 certificate)
        {
            return certificate.Verify() && certificate.Issuer.Contains("O=Microsoft Corporation");
        }
    }
}
```
