---
title: ポリシーを使用してデバイスの一覧を更新する
description: 指定された顧客の構成ポリシーを使用してデバイスの一覧を更新する方法。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 18ec280995b978a5ac62d3d7288337c1307a6643
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927579"
---
# <a name="update-a-list-of-devices-with-a-policy"></a>ポリシーを使用してデバイスの一覧を更新する

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター

指定された顧客の構成ポリシーを使用してデバイスの一覧を更新する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- ポリシー識別子。

- 更新するデバイスのデバイス id。

## <a name="c"></a>C\#

指定された構成ポリシーを使用してデバイスの一覧を更新するには、まず、次のコード例に示すように、型 [KeyValuePair/dotnet/api/KeyValuePair-2) [**(Policycategory,**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory) string) の [list/dotnet/api/] をインスタンス化して、適用するポリシーを追加します。 ポリシーのポリシー識別子が必要になります。

次に、ポリシーを使用して更新する [**device**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device] オブジェクトの一覧を作成します。デバイス id と、適用するポリシーを含む一覧をデバイスごとに指定します。 次に、[**Devicepolicyupdaterequest**) オブジェクトをインスタンス化し、[**Devices**/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices)] プロパティをデバイスオブジェクトの一覧に設定します。

デバイスポリシーの更新要求を処理するには、顧客識別子を使用して [**iaggregatepartner.customers. ById**/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) メソッドを呼び出し、指定された顧客の操作へのインターフェイスを取得します。 次に、[**Devicepolicy**/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy)] プロパティを取得して、顧客のデバイスコレクション操作へのインターフェイスを取得します。 最後に、DevicePolicyUpdateRequest オブジェクトを使用して [**update**) メソッドを呼び出し、デバイスをポリシーで更新します。

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;
string selectedDeviceId;

// Indicate the policy to apply to the list of devices.
List<KeyValuePair<PolicyCategory, string>>
    policyToBeAdded = new List<KeyValuePair<PolicyCategory, string>>
{
    new KeyValuePair<PolicyCategory, string>
        (PolicyCategory.OOBE, selectedConfigurationPolicyId)
};

// Create a list of devices to be updated with a policy.
List<Device> devices = new List<Device>
{
    new Device
    {
        Id = selectedDeviceId,
        Policies=policyToBeAdded
    }
};

// Instantiate a DevicePolicyUpdateRequest object.
DevicePolicyUpdateRequest
    devicePolicyUpdateRequest = new DevicePolicyUpdateRequest
{
    Devices = devices
};

// Process the DevicePolicyUpdateRequest.
var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DevicePolicy.Update(devicePolicyUpdateRequest);
```

**サンプル**: [コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル **クラス**: UpdateDevicesPolicy.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法    | 要求 URI                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

要求の作成時には、次のパスパラメーターを使用します。

| 名前        | 種類   | 必須 | 説明                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | はい      | 顧客を識別する GUID 形式の文字列。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

要求本文には、 [Devicepolicyupdaterequest](device-deployment-resources.md#devicepolicyupdaterequest) リソースが含まれている必要があります。

### <a name="request-example"></a>要求の例

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/DevicePolicyUpdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 363
Expect: 100-continue
Connection: Keep-Alive

{
    "Devices": [{
            "Id": "9993-8627-3608-6844-6369-4361-72",
            "SerialNumber": null,
            "ProductKey": null,
            "HardwareHash": null,
            "Policies": [{
                    "Key": "o_o_b_e",
                    "Value": "15a04610-9229-4e80-94e0-0e826a09c9e2"
                }
            ],
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DevicePolicyUpdateRequest"
    }
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答には、このバッチ処理の状態を取得するために使用できる URI を持つ **場所** ヘッダーが含まれます。 他の関連する REST Api で使用するために、この URI を保存します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/a15f3996-620a-4404-9f1f-4c2de78de0de
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CV: rCXyd8Z/lUSxUd0P.0
MS-ServerId: 020021921
Date: Thu, 28 Sep 2017 21:33:05 GMT
```
