---
title: デバイスの一覧を指定された顧客の既存のバッチにアップロードする
description: 指定された顧客の既存のバッチに、デバイスに関する情報の一覧をアップロードする方法。 これにより、既に作成されているデバイスバッチにデバイスが関連付けられます。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a3f6522b31d296e10c66cb45b3684eae3e0c25ab
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926432"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a>デバイスの一覧を指定された顧客の既存のバッチにアップロードする

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター

指定された顧客の既存のバッチに、デバイスに関する情報の一覧をアップロードする方法。 これにより、既に作成されているデバイスバッチにデバイスが関連付けられます。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- デバイスのバッチ識別子。

- 個々のデバイスに関する情報を提供するデバイスリソースの一覧。

## <a name="c"></a>C\#

既存のデバイスバッチにデバイスの一覧をアップロードするには、まず、種類が [**デバイス**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device] の新しい [list/dotnet/api/] をインスタンス化し、リストにデバイスを設定します。 各デバイスを識別するには、少なくとも次の設定されたプロパティの組み合わせが必要です。

- [**ハードウェアハッシュ**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)。

- [**ハードウェアハッシュ**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**シリアル**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) です。

- [**ハードウェアハッシュ**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**/Dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**シリアル**の/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) です。

- [**ハードウェアハッシュ**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) のみです。

- [**ProductKey**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) のみです。

- [**シリアル**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**/Dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname) です。

次に、顧客識別子を使用して [**iaggregatepartner.customers. ById**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) メソッドを呼び出し、指定された顧客の操作に対するインターフェイスを取得します。 次に、デバイスのバッチ識別子を使用して [**Devicebatches**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) メソッドを呼び出し、指定されたバッチの操作のインターフェイスを取得します。 最後に、デバイスの一覧を使用してデバイスバッチにデバイスを追加するデバイスの一覧を使用して、**[/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) または [****createasync**/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) メソッドを呼び出します。

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash1234",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    },

    new Device
    {
        HardwareHash = "DummyHash12345",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    }
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Create(devicesToBeUploaded);
```

**サンプル**: [コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル **クラス**: CreateDevices.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法   | 要求 URI                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

要求の作成時には、次のパスとクエリパラメーターを使用します。

| 名前           | 種類   | 必須 | 説明                                           |
|----------------|--------|----------|-------------------------------------------------------|
| customer-id    | string | はい      | 顧客を識別する GUID 形式の文字列。 |
| devicebatch-id | string | はい      | デバイスバッチを識別する文字列識別子。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

要求本文には、 [デバイス](device-deployment-resources.md#device) オブジェクトの配列が含まれている必要があります。 デバイスを識別するための次のフィールドの組み合わせが受け入れられます。

- ハードウェアハッシュ + productKey。
- ハードウェアハッシュ + シリアル
- ハードウェアハッシュ + productKey + シリアル。
- ハードウェアハッシュのみ。
- productKey のみです。
- シリアルの + oemManufacturerName + modelName。

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches/Test/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 482
Expect: 100-continue

[{
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash1234",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }, {
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash12345",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }
]
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答には、デバイスのアップロードステータスを取得するために使用できる URI を含む **場所** ヘッダーが含まれます。 他の関連する REST Api で使用するために、この URI を保存します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/16c00110-e79a-433d-aa28-f69dd60df671
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CV: OBkGN9pSN0a5xvua.0
MS-ServerId: 101112012
Date: Thu, 28 Sep 2017 20:08:46 GMT
```
