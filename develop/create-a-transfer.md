---
title: 転送を作成する
description: 顧客のサブスクリプションの転送を作成する方法。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e77711f2bda6d4e5af536ed2658df63241462c31
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82154814"
---
# <a name="create-a-transfer"></a>転送を作成する

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナーセンターの[ダッシュボード](https://partner.microsoft.com/dashboard)で確認できます。 パートナーセンターメニューの [ **CSP** ] を選択し、[ **Customers**] をクリックします。 [Customer] リストから顧客を選択し、[Account] \ (**アカウント**\) を選択します。 お客様のアカウントページで、[**お客様のアカウント情報**] セクションで**Microsoft ID**を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求の構文

| 認証方法   | 要求 URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1                    |

### <a name="uri-parameter"></a>URI パラメーター

次のパス パラメーターを使用して顧客を指定します。

| 名前            | Type     | 必須 | 説明                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **顧客 id** | string   | はい      | 顧客を識別する GUID 形式の顧客 id。             |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

次の表では、要求本文の[Transferentity](transfer-entity-resources.md)プロパティについて説明します。

| プロパティ              | Type          | 必須  | 説明                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| id                    | string        | いいえ    | TransferEntity が正常に作成されたときに提供される transferEntity 識別子。                               |
| createdTime           | DateTime      | いいえ    | TransferEntity が作成された日付 (日付/時刻形式)。 TransferEntity の作成が正常に完了したときに適用されます。      |
| lastModifiedTime      | DateTime      | いいえ    | TransferEntity が最後に更新された日付 (日付/時刻形式)。 TransferEntity の作成が正常に完了したときに適用されます。 |
| lastModifiedUser      | string        | いいえ    | TransferEntity を最後に更新したユーザー。 TransferEntity の作成が正常に完了したときに適用されます。                          |
| customerName          | string        | いいえ    | 省略可能。 サブスクリプションを転送する顧客の名前。                                              |
| 顧客 Tenantid      | string        | いいえ    | 顧客を識別する GUID 形式の顧客 id。 TransferEntity の作成が正常に完了したときに適用されます。         |
| partnertenantid       | string        | いいえ    | パートナーを識別する GUID 形式のパートナー id。                                                                   |
| sourcePartnerName     | string        | いいえ    | 省略可能。 譲渡を開始するパートナー組織の名前。                                           |
| sourcePartnerTenantId | string        | はい   | 転送を開始するパートナーを識別する GUID 形式のパートナー id。                                           |
| targetPartnerName     | string        | いいえ    | 省略可能。 譲渡の対象となるパートナーの組織の名前。                                         |
| targetPartnerTenantId | string        | はい   | 転送の対象となるパートナーを識別する GUID 形式のパートナー id。                                  |
| lineItems             | オブジェクトの配列 | はい| [Transferlineitem](transfer-entity-resources.md#transferlineitem)リソースの配列。                                   |
| status                | string        | いいえ    | TransferEntity の状態。 有効な値は、"アクティブ" (削除/送信可能) および "完了" (既に完了している) です。 TransferEntity の作成が正常に完了したときに適用されます。|

次の表では、要求本文の[Transferlineitem](transfer-entity-resources.md#transferlineitem)プロパティについて説明します。

|      プロパティ       |            Type             | 必須 | 説明                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| id                   | string                     | いいえ       | 転送明細項目の一意の識別子。 TransferEntity の作成が正常に完了したときに適用されます。|
| subscriptionId       | string                     | はい      | サブスクリプションの識別子です。                                                                         |
| 数量             | INT                        | いいえ       | ライセンスまたはインスタンスの数。                                                                 |
| billingCycle         | Object                     | いいえ       | 現在の期間に設定されている請求サイクルの種類。                                                |
| friendlyName         | string                     | いいえ       | 省略可能。 明確に区別できるように、パートナーによって定義された項目のフレンドリ名。                |
| partnerIdOnRecord    | string                     | いいえ       | 転送が受け入れられたときに発生する、購入時の PartnerId (MPNID)。              |
| offerId              | string                     | いいえ       | プラン ID。                                                                                |
| addonItems           | **Transferlineitem**オブジェクトの一覧 | いいえ | 転送されるベースサブスクリプションと共に転送されるアドオンの transferEntity 行項目のコレクション。 TransferEntity の作成が正常に完了したときに適用されます。|
| transferError        | string                     | いいえ       | エラーが発生した場合に transferEntity が受け入れられた後に適用されます。                                        |
| status               | string                     | いいえ       | TransferEntity 内の lineitem の状態。                                                    |

### <a name="request-example"></a>要求の例

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは、応答本文[で設定さ](transfer-entity-resources.md)れた転送リソースを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[エラー コード](error-codes.md)に関するページを参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
