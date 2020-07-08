---
title: 指定された顧客のデバイスを削除する
description: 指定された顧客に属するデバイスを削除する方法。
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2e1727b36f7775f59c191172c5514f0accbf3091
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094162"
---
# <a name="delete-a-device-for-the-specified-customer"></a>指定された顧客のデバイスを削除する

**適用対象:**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター

この記事では、指定された顧客に属するデバイスを削除する方法について説明します。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

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

| 認証方法     | 要求 URI                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1  |

#### <a name="uri-parameters"></a>URI パラメーター

要求の作成時には、次のパスパラメーターを使用します。

| 名前           | Type   | 必須 | 説明                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| customer-id    | string | はい      | 顧客を識別する GUID 形式の文字列。              |
| devicebatch-id | string | はい      | デバイスを含むバッチのデバイスバッチ識別子。 |
| device-id      | string | はい      | デバイス識別子。                                             |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

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

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

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
