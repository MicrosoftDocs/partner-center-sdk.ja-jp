---
title: 指定されたバッチと顧客のデバイスの一覧を取得する
description: 顧客に対して指定されたデバイスバッチ内のデバイスとデバイスの詳細のコレクションを取得する方法。
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 125d1b4e239f69ae2dfc9667f5d009bab9f415b2
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927663"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a>指定されたバッチと顧客のデバイスの一覧を取得する

**適用対象:**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター

この記事では、指定した顧客について、指定したデバイスバッチ内のデバイスのコレクションを取得する方法について説明します。 各デバイスリソースには、デバイスに関する詳細が含まれています。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- デバイスバッチ識別子。

## <a name="c"></a>C\#

指定された顧客について、指定されたデバイスバッチ内のデバイスのコレクションを取得するには、次のようにします。

1. 顧客 ID と共に [**iaggregatepartner.customers. ById**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) メソッドを呼び出して、指定された顧客の操作に対するインターフェイスを取得します。

2. [**ById**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) メソッドを呼び出して、指定されたバッチのデバイスバッチコレクション操作へのインターフェイスを取得します。

3. [**Devices**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices] プロパティを取得して、バッチのデバイスコレクション操作へのインターフェイスを取得します。

4. [**Get**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get)] または [**GetAsync**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync] メソッドを呼び出して、デバイスのコレクションを取得します。

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

例については、以下を参照してください。

- サンプル: [コンソール テスト アプリ](console-test-app.md)
- プロジェクト: **パートナーセンター SDK のサンプル**
- クラス: **GetDevices.cs**

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1 |

#### <a name="uri-parameters"></a>URI パラメーター

要求の作成時には、次のパスパラメーターを使用します。

| 名前           | 種類   | 必須 | 説明                                           |
|----------------|--------|----------|-------------------------------------------------------|
| customer-id    | string | はい      | 顧客を識別する GUID 形式の文字列。 |
| devicebatch-id | string | はい      | デバイスバッチを識別する文字列識別子。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

なし

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には、 [デバイス](device-deployment-resources.md#device) リソースのページングされたコレクションが含まれます。 コレクションには、ページ内の100デバイスが含まれます。 100デバイスの次のページを取得するには、応答本文の continuationToken を ContinuationToken ヘッダーとして後続の要求に含める必要があります。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、「 [パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 1742
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 2,
    "items":
    [{
            "id": "7c141ea9-2816-4e15-a819-53f6856499ff",
            "serialNumber": "2R9-ZNP67",
            "productKey": "00329-00000-0003-AA6069",
            "modelName": "Precision WorkStation T7500",
            "oemManufacturerName":"Dell Inc.",
            "policies":[{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate":"2017-08-09T14:43:26.0092288-07:00",
            " attributes": {
                "objectType": "Device"
            }
        }, {
            "id": "e528a62f-5031-49f4-bea7-5fafe47388fd",
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "modelName": "HP Z420 Workstation",
            "oemManufacturerName": "Hewlett-Packard",
            "policies": [{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate": "2017-08-09T14:35:51.3126144-07:00",
            "attributes": {
                "objectType": "Device"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
