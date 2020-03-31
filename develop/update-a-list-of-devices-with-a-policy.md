---
title: ポリシーを使用してデバイスの一覧を更新する
description: 指定された顧客の構成ポリシーを使用してデバイスの一覧を更新する方法。
ms.assetid: D68DAE8B-EFBC-4C71-8CB4-3ADA8D45DDBA
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c3c94b53eb30e648862bac4d1ea46bbfdd2cb643
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414819"
---
# <a name="update-a-list-of-devices-with-a-policy"></a>ポリシーを使用してデバイスの一覧を更新する


**適用対象**

- Partner Center
- Microsoft Cloud ドイツのパートナー センター

指定された顧客の構成ポリシーを使用してデバイスの一覧を更新する方法。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客識別子。
- ポリシー識別子。
- 更新するデバイスのデバイス id。

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


指定された構成ポリシーを使用してデバイスの一覧を更新するには、まず、次のコード例に示すように、 [KeyValuePair](https://docs.microsoft.com/dotnet/api/system.collections.generic.keyvaluepair-2)[ **(policycategory,** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)String) 型の[リスト](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1)をインスタンス化し、適用するポリシーを追加します。 ポリシーのポリシー識別子が必要になります。

次に、ポリシーを使用して更新する[**デバイス**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device)オブジェクトの一覧を作成します。デバイス id と、適用するポリシーを含む一覧をデバイスごとに指定します。 次に、 [**Devicepolicyupdaterequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest)オブジェクトをインスタンス化し、 [**Devices**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices)プロパティをデバイスオブジェクトの一覧に設定します。

デバイスポリシーの更新要求を処理するには、顧客識別子を使用して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出し、指定された顧客の操作へのインターフェイスを取得します。 次に、 [**Devicepolicy**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy)プロパティを取得して、顧客のデバイスコレクション操作へのインターフェイスを取得します。 最後に、DevicePolicyUpdateRequest オブジェクトを使用して[**update**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update)メソッドを呼び出し、デバイスをポリシーで更新します。

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

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: UpdateDevicesPolicy.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>要求


**要求の構文**

| メソッド    | 要求 URI                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| **KB830347** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1 |

 

**URI パラメーター**

要求の作成時には、次のパスパラメーターを使用します。

| Name        | 種類   | 必須 | 説明                                           |
|-------------|--------|----------|-------------------------------------------------------|
| 顧客 id | string | はい      | 顧客を識別する GUID 形式の文字列。 |

 

**要求ヘッダー**

- 詳細については、「[パートナーセンターの REST ヘッダー](headers.md) 」を参照してください。

**要求本文**

要求本文には、 [Devicepolicyupdaterequest](device-deployment-resources.md#devicepolicyupdaterequest)リソースが含まれている必要があります。

**要求の例**

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

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>応答


成功した場合、応答には、このバッチ処理の状態を取得するために使用できる URI を持つ**場所**ヘッダーが含まれます。 他の関連する REST Api で使用するために、この URI を保存します。

**応答成功およびエラーコード**

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

**応答の例**

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

 

 




