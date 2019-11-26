---
title: 指定された顧客の新しいバッチを作成するために、デバイスの一覧をアップロードします
description: 指定された顧客の新しいバッチを作成するために、デバイスに関する情報の一覧をアップロードする方法。 これにより、ゼロタッチ展開で登録するためのデバイスバッチが作成され、デバイスとデバイスバッチが指定の顧客に関連付けられます。
ms.assetid: 94DB98F2-2188-46BB-97BA-100B8C94F120
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: aa57a20e30d7e71f60dd0733b6f5bfead9accfca
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486312"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a>指定された顧客の新しいバッチを作成するために、デバイスの一覧をアップロードします

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター

指定された顧客の新しいバッチを作成するために、デバイスに関する情報の一覧をアップロードする方法。 これにより、ゼロタッチ展開で登録するためのデバイスバッチが作成され、デバイスとデバイスバッチが指定の顧客に関連付けられます。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリ + ユーザー資格情報を使用した認証がサポートされます。 パートナーセンター Api でアプリとユーザー認証を使用する場合は、[セキュリティで保護されたアプリモデル](enable-secure-app-model.md)に従います。
- 顧客識別子。
- 個々のデバイスに関する情報を提供するデバイスリソースの一覧。

## <a name="c"></a>C\#

新しいデバイスバッチを作成するためにデバイスの一覧をアップロードするには、次のようにします。

1. [**デバイス**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device)の種類の新しい[リスト](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1)をインスタンス化し、リストに追加します。 各デバイスを識別するには、少なくとも次の設定されたプロパティの組み合わせが必要です。

    - [**ハードウェアハッシュ**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)。
    - [**ハードウェアハッシュ**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**シリアル**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)。
    - [**ハードウェアハッシュ**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**シリアル**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)になります。
    - [**ハードウェアハッシュ**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)のみ。
    - [**ProductKey**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)のみです。
    - [**シリアル**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname)。

2. [**Devicebatchの request**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest)オブジェクトをインスタンス化し、 [**batchid**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid)プロパティを任意の一意の名前に設定し、 [**devices**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices)プロパティをアップロードするデバイスの一覧に設定します。

3. 顧客 id を指定して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出し、指定された顧客の操作へのインターフェイスを取得することによって、デバイスのバッチ作成要求を処理します。

4. [**Devicebatches**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection)を呼び出します。バッチを作成するには、デバイスのバッチ作成要求を使用して、create または[**createasync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection)メソッドを呼び出します。

```csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash123",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "1R9-ZNP67"
    }
};

DeviceBatchCreationRequest
    newDeviceBatch = new DeviceBatchCreationRequest
{
    BatchId = "SDKTestDeviceBatch",
    Devices = devicesToBeUploaded
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Create(newDeviceBatch);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: CreateDeviceBatch.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド   | 要求 URI                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **投稿** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1 |

#### <a name="uri-parameter"></a>URI パラメーター

要求の作成時には、次のパスパラメーターを使用します。

| 名前        | 種類   | 必須 | 説明                                           |
|-------------|--------|----------|-------------------------------------------------------|
| 顧客 id | string | 〇      | 顧客を識別する GUID 形式の文字列。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

要求本文には、 [Devicebatchの要求](device-deployment-resources.md#devicebatchcreationrequest)リソースが含まれている必要があります。

### <a name="request-example"></a>要求の例

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
    "BatchId": "SDKTestDeviceBatch",
    "Devices": [{
            "Id": null,
            "SerialNumber": "1R9-ZNP67",
            "ProductKey": "00329-00000-0003-AA606",
            "HardwareHash": "DummyHash123",
            "Policies": null,
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DeviceBatchCreationRequest"
    }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答には、デバイスのアップロードステータスを取得するために使用できる URI を含む**場所**ヘッダーが含まれます。 他の関連する REST Api で使用するために、この URI を保存します。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

#### <a name="response-example"></a>応答の例

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/beba2053-5401-46ff-9223-7e841ed78fbf
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2017 20:35:35 GMT
```
