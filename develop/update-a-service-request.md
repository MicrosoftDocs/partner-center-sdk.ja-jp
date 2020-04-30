---
title: サービス リクエストを更新する
description: お客様の代わりに、クラウドソリューションプロバイダーによって Microsoft に提出された既存のカスタマーサービスリクエストを更新する方法。
ms.assetid: 09C13775-739B-4CB9-9442-456E17F91452
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: ca618afa6e5dc2b6db141ec8a590554b9592eb94
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157944"
---
# <a name="update-a-service-request"></a>サービス リクエストを更新する

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

お客様の代わりに、クラウドソリューションプロバイダーによって Microsoft に提出された既存のカスタマーサービスリクエストを更新する方法。

パートナーセンターのダッシュボードでは、最初に[顧客を選択](get-a-customer-by-name.md)することでこの操作を実行できます。 次に、左側のサイドバーで [**サービス管理**] を選択します。 [**サポート要求**] ヘッダーの下で、対象のサービス要求を選択します。 完了するには、サービス要求に必要な変更を行い、[送信] を選択し**ます。**

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリ + ユーザー資格情報のみを使用した認証がサポートされます。

- サービス要求 ID。

## <a name="c"></a>C\#

顧客のサービス要求を更新するには、サービス要求 id を指定して[**IServiceRequestCollection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid)メソッドを呼び出し、サービス要求インターフェイスを特定して返します。 次に、 [**IServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch)または Patch [**async**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync)メソッドを呼び出して、サービス要求を更新します。 更新された値を提供するには、新しい空の[**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest)オブジェクトを作成し、変更するプロパティ値のみを設定します。 次に、そのオブジェクトを Patch または Patch Async メソッドの呼び出しで渡します。

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: UpdatePartnerServiceRequest.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法    | 要求 URI                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

サービス要求を更新するには、次の URI パラメーターを使用します。

| 名前                  | Type     | 必須 | 説明                                 |
|-----------------------|----------|----------|---------------------------------------------|
| **servicerequest-id** | **guid** | Y        | サービス要求を識別する GUID。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

要求本文には、 [ServiceRequest](service-request-resources.md)リソースが含まれている必要があります。 必要な値は、更新される値のみです。

### <a name="request-example"></a>要求の例

```http
PATCH https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 508
Expect: 100-continue

{
    "Id": null,
    "Title": null,
    "Description": null,
    "Severity": "unknown",
    "SupportTopicId": null,
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": {
        "CreatedByName": null,
        "CreatedDate": null,
        "Text": "Sample Note"
    },
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で更新されたプロパティを含む**サービス要求**リソースを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 566
Content-Type: application/json; charset=utf-8
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CV: rjLONPum/Uq94UQA.0
MS-ServerId: 030011719
Date: Mon, 09 Jan 2017 23:31:15 GMT

{
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "supportTopicName": "Cannot manage my profile",
    "id": "616122292874576",
    "status": "open",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1"
    },
    "productId": "15960",
    "createdDate": "2016-12-22T20:31:17.24Z",
    "lastModifiedDate": "2017-01-09T23:31:15.373Z",
    "lastClosedDate": "0001-01-01T00:00:00",
    "notes": [{
            "createdByName": "Account",
            "createdDate": "2017-01-09T23:31:15.373",
            "text": "Sample Note"
        }
    ],
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```
