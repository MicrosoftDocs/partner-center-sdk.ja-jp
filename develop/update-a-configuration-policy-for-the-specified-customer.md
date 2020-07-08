---
title: 指定された顧客の構成ポリシーを更新する
description: 指定された顧客に対して指定された構成ポリシーを更新する方法。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5fe3b30dd62fb0d2653f52d875310ff302f36bd2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095960"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a>指定された顧客の構成ポリシーを更新する

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター

指定された顧客に対して指定された構成ポリシーを更新する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

- ポリシー識別子。

## <a name="c"></a>C\#

指定された顧客の既存の構成ポリシーを更新するには、次のコードスニペットに示すように、新しい[**configurationpolicy**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy)オブジェクトをインスタンス化します。 この新しいオブジェクトの値は、既存のオブジェクト内の対応する値に置き換えられます。 次に、顧客 ID を指定して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)メソッドを呼び出し、指定された顧客の操作に対するインターフェイスを取得します。 次に、ポリシー ID を指定して[**ById**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid)メソッドを呼び出し、指定したポリシーの構成ポリシー操作へのインターフェイスを取得します。 最後に、Patch または[**Patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) [**async**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync)メソッドを呼び出して、構成ポリシーを更新します。

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

**サンプル**:[コンソールテストアプリ](console-test-app.md)。 **プロジェクト**: パートナーセンター SDK サンプル**クラス**: UpdateConfigurationPolicy.cs

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

要求の作成時には、次のパスパラメーターを使用します。

| 名前        | Type   | 必須 | 説明                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| customer-id | string | はい      | 顧客を識別する GUID 形式の文字列。         |
| ポリシー-id   | string | はい      | 更新するポリシーを識別する GUID 形式の文字列。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

要求本文には、ポリシー情報を提供するオブジェクトが含まれている必要があります。

| 名前            | Type             | 必須 | 更新可能 | 説明                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| id              | string           | はい      | いいえ        | ポリシーを識別する GUID 形式の文字列。                                                                                                    |
| name            | string           | はい      | はい       | ポリシーのフレンドリ名。                                                                                                                         |
| category        | string           | はい      | いいえ        | ポリシーカテゴリ。                                                                                                                                     |
| description     | 文字列           | いいえ       | はい       | ポリシーの説明。                                                                                                                                  |
| 割り当てられたデバイス | number           | いいえ       | いいえ        | デバイスの数。                                                                                                                                   |
| policySettings  | 文字列の配列 | はい      | はい       | ポリシー設定は、"none"、"oem プレインストールを削除する \_ \_ "、"oobe \_ user \_ not \_ local \_ admin"、"簡易設定をスキップする \_ \_ "、"oem 登録をスキップする"、" \_ \_ eula をスキップする" \_ です。 |

### <a name="request-example"></a>要求の例

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、応答本文には新しいポリシーの[Configurationpolicy](device-deployment-resources.md#configurationpolicy)リソースが含まれます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
