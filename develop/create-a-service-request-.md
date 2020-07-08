---
title: サービス要求を作成する
description: パートナーセンターのサービス要求を作成する方法。
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dc38c613f19340b84389b82e939615504538ec97
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094547"
---
# <a name="create-a-service-request"></a>サービス要求を作成する

**適用対象:**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーセンターのサービス要求を作成する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザーの資格情報を使用した認証のみがサポートされます。

- サポートトピック ID。 サポートトピック ID がない場合は、「[サービス要求のサポートトピックを取得](get-service-request-support-topics--pending-.md)する」を参照してください。

## <a name="c"></a>C\#

サービス要求を作成するには:

1. タイトル、説明、重大度、サポートトピック id を使用して、 [**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest)オブジェクトを作成し、設定します。追加情報を追加するために、 [**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest)オブジェクトはオプションの[**メモ**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.notes)のコレクションをサポートしていますが、アップロードするファイルへのリンクはサポートしていません。

2. オブジェクトが作成されたら、 [**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.ipartnerservicerequestcollection.create)メソッドを呼び出し、新しく作成された ServiceRequest オブジェクトと、サービス要求を作成した組織のロケール (エージェントのロケール) を含む文字列を渡します。

### <a name="c-example"></a>C の \# 例

``` csharp
// IAggregatePartner partnerOperations;
// string supportTopicId;

ServiceRequest serviceRequestToCreate = new ServiceRequest()
{
    Title = "TrialSR",
    Description = "Ignore this SR",
    Severity = ServiceRequestSeverity.Critical,
    SupportTopicId = supportTopicId
};

ServiceRequest serviceRequest = partnerOperations.ServiceRequests.Create(serviceRequestToCreate, "en-US");
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: CreatePartnerServiceRequest.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法   | 要求 URI                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{agent-locale} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

次の URI パラメーターを使用して、エージェントのロケールを識別します。

| 名前             | Type       | 必須 | 説明                                                  |
|------------------|------------|----------|--------------------------------------------------------------|
| **エージェント-ロケール** | **string** | Y        | サービス要求を作成する組織のロケール。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

次の表では、要求本文の必須プロパティと省略可能なプロパティについて説明します。

| 名前             | Type                                                                        | 必須 | 説明                                                                          |
|------------------|-----------------------------------------------------------------------------|----------|--------------------------------------------------------------------------------------|
| タイトル            | string                                                                      | Y        | サービス要求のタイトル。                                                           |
| 説明      | string                                                                      | Y        | 説明です。                                                                     |
| 重大度         | string                                                                      | Y        | 重大度: "unknown"、"critical"、"中"、または "最小"。                       |
| サポートトピック Id   | string                                                                      | Y        | サポートトピックの id。                                                         |
| サポートトピック名 | string                                                                      | N        | サポートトピックの名前。                                                       |
| Id               | string                                                                      | N        | サービス要求の id。                                                       |
| 状態           | string                                                                      | N        | サービス要求の状態: "none"、"open"、"closed"、または "attention \_ 必要"。 |
| Organization     | [ServiceRequestOrganization](service-request-resources.md#servicerequestorganization) | N        | サービス要求が作成される組織。                               |
| PrimaryContact   | [ServiceRequestContact](service-request-resources.md#servicerequestcontact)           | N        | サービスリクエストに関する主要連絡先。                                              |
| LastUpdatedBy    | [ServiceRequestContact](service-request-resources.md#servicerequestcontact)           | N        | サービスリクエストの変更については、"最終更新者" に問い合わせます。                        |
| ProductName      | string                                                                      | N        | サービス要求に対応する製品の名前。                     |
| ProductId        | string                                                                      | N        | 製品の id。                                                               |
| CreatedDate      | date                                                                        | N        | サービス要求の作成日。                                          |
| LastModifiedDate | date                                                                        | N        | サービス要求が最後に変更された日付。                                 |
| LastClosedDate   | date                                                                        | N        | サービス要求が最後に閉じられた日付。                                   |
| FileLinks        | [FileInfo](utility-resources.md#fileinfo)リソースの配列               | N        | サービス要求に関連するファイルリンクのコレクション。                    |
| NewNote          | [ServiceRequestNote](service-request-resources.md#servicerequestnote)                 | N        | 既存のサービス要求にメモを追加できます。                                  |
| メモ            | [ServiceRequestNotes](service-request-resources.md#servicerequestnote)の配列       | N        | サービス要求に追加されるメモのコレクション。                                  |
| CountryCode      | string                                                                      | N        | サービス要求に対応する国。                                    |
| 属性       | object                                                                      | N        | "ObjectType": "ServiceRequest" が含まれています。                                             |

次の表では、要求本文に必要なプロパティについて説明します。

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/servicerequests/en-US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 55f86bfb-d3bb-4fe4-9f01-2fdaef11a81f
MS-CorrelationId: ae43859b-591d-47ea-9fd1-028b4c799118
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 474
Expect: 100-continue

{
    "Id": null,
    "Title": "TrialSR",
    "Description": "Ignore this SR",
    "Severity": "critical",
    "SupportTopicId": "32444671",
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
    "NewNote": null,
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文の**サービス要求**リソースプロパティを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 201 Created
Content-Length: 721
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae43859b-591d-47ea-9fd1-028b4c799118
MS-RequestId: 55f86bfb-d3bb-4fe4-9f01-2fdaef11a81f
MS-CV: vB9EuWs/ukaxQmuV.0
MS-ServerId: 101112616
Date: Thu, 22 Dec 2016 20:31:14 GMT

 {
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "id": "616122292874576",
    "status": "none",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1",
        "phoneNumber": "2398391056"
    },
    "primaryContact": {
        "organization": {
            "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "name": "TEST_TEST_BugBash1",
            "phoneNumber": "2398391056"
        },
        "contactId": "bb4ebcf5-d84c-4b35-8469-f4cfa4ac909e",
        "lastName": "Account",
        "email": "admin@testtestbugbash1.onmicrosoft.com",
        "phoneNumber": "2066017143"
    },
    "createdDate": "0001-01-01T00:00:00",
    "lastModifiedDate": "0001-01-01T00:00:00",
    "lastClosedDate": "0001-01-01T00:00:00",
    "countryCode": "US",
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```
