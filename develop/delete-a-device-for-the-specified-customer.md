---
title: 指定された顧客のデバイスを削除します
description: 指定された顧客に属するデバイスを削除する方法。
ms.assetid: 44F06D4B-E9DE-470F-BAE2-15205CC7C699
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: c5a8a1e69bd79b9444ec19bcac3c0b62374fbd3f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489902"
---
# <a name="delete-a-device-for-the-specified-customer"></a>指定された顧客のデバイスを削除します

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター

このトピックでは、指定された顧客に属するデバイスを削除する方法について説明します。

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客識別子。
- デバイスのバッチ識別子。
- デバイス識別子。

## <a name="c"></a>C\#

指定された顧客のデバイスを削除するには:

1. 顧客識別子を使用して[**iaggregatepartner.customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出し、顧客の操作に対するインターフェイスを取得します。
2. デバイスバッチ識別子を使用して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid)メソッドを呼び出し、指定されたバッチの操作へのインターフェイスを取得します。
3. [**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid)メソッドを呼び出して、指定されたデバイスで操作するインターフェイスを取得します。
4. Batch からデバイスを削除するには、 [**delete**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete)または[**deleteasync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync)メソッドを呼び出します。

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: DeleteDevice.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| メソッド     | 要求 URI                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| DELETE     | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1  |

#### <a name="uri-parameters"></a>URI パラメーター

要求の作成時には、次のパスパラメーターを使用します。

| 名前           | 種類   | 必須 | 説明                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| 顧客 id    | string | 〇      | 顧客を識別する GUID 形式の文字列。              |
| devicebatch-id | string | 〇      | デバイスを含むバッチのデバイスバッチ識別子。 |
| デバイス id      | string | 〇      | デバイス識別子。                                             |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

### <a name="request-body"></a>要求本文

なし

### <a name="request-example"></a>要求の例

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices/7b11cd8b-dd1e-4840-8c4a-84215e4de782 HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答は**204 コンテンツ**ステータスコードを返しません。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。 ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```