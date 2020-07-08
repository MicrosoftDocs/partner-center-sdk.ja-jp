---
title: 指定された顧客のデバイス バッチの一覧を取得する
description: 指定された顧客のデバイスバッチのコレクションを取得する方法。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d1667b1be4a3063f846b15052427ffdedb33754b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097445"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a>指定された顧客のデバイス バッチの一覧を取得する

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター

指定された顧客のデバイスバッチのコレクションを取得する方法。

各デバイスバッチには、ゼロタッチ展開に登録されているデバイスに関する概要ステータス情報が含まれています。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="c"></a>C\#

指定された顧客のデバイスバッチのコレクションを取得するには、まず、顧客 ID を指定して[**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出し、指定された顧客に対する操作のインターフェイスを取得します。 次に、 [**devicebatches**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches)プロパティの値を取得して、デバイスのバッチコレクション操作へのインターフェイスを取得します。 最後に、 [**Get**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get)または[**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync)メソッドを呼び出して、コレクションを取得します。

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: GetDevicesBatches.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

要求の作成時には、次のパスパラメーターを使用します。

| 名前        | Type   | 必須 | 説明                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | はい      | 顧客を識別する GUID 形式の文字列。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には[Devicebatch](device-deployment-resources.md#devicebatch)リソースのコレクションが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 339
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "Test batch",
            "status": "finished",
            "creationDate": "2017-07-25T01:51:00",
            "devicesCount": 5,
            "devicesLink": {
                "uri": "/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/Test batch/devices",
                "method": "GET",
                "headers": []
            },
            "attributes": {
                "objectType": "DeviceBatch"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
