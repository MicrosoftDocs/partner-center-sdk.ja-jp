---
title: 顧客の譲渡を取得する
description: 顧客の譲渡の一覧を取得する方法。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4a25a9f6ccba0a3d64934b23ccd83a535da05e4a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86093955"
---
# <a name="get-a-customers-transfers"></a>顧客の譲渡を取得する

**適用対象**

- パートナー センター

顧客の譲渡の一覧を取得する方法。

## <a name="prerequisites"></a>前提条件

- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。

- 顧客 ID です (`customer-tenant-id`)。 お客様の ID がわからない場合は、パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で検索できます。 パートナー センター メニューの **[CSP]** を選択し、 **[顧客]** を選択します。 顧客一覧からお客様を選び、 **[アカウント]** を選択します。 お客様のアカウント ページで、 **[顧客のアカウント情報]** セクションの **Microsoft ID** を探します。 Microsoft ID は、顧客 ID (`customer-tenant-id`) と同じです。

### <a name="request-syntax"></a>要求の構文

| 認証方法  | 要求 URI                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/transfers HTTP/1.1 |

### <a name="uri-parameter"></a>URI パラメーター

次の表に、すべてのサブスクリプションを取得するために必要なクエリパラメーターを示します。

| 名前               | Type   | 必須 | 説明                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| customer-tenant-id | string | はい      | 顧客を識別する GUID 形式の文字列。 |

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca2cdd2c-7eb8-4a2e-cdd7-2848752e801a
MS-CorrelationId: dec58181-67b5-4831-c2c9-2fa099122f5d
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは、応答本文内の[Transferentity](transfer-entity-resources.md)リソースのリストを返します。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。 このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 13828
Content-Type: application/json
MS-CorrelationId: dec58181-67b5-4831-c2c9-2fa099122f5d
MS-RequestId: ca2cdd2c-7eb8-4a2e-cdd7-2848752e801a
Date: Fri, 27 Mar 2020 17:50:34 GMT

[
  {
    "id": "ab724652-3442-4912-8615-61525bb9903d",
    "status": "Reject",
    "createdTime": "2019-10-09T22:44:13.5411441Z",
    "lastModifiedTime": "2020-02-20T21:27:59Z",
    "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
    "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "sourcePartnerName": "Test_Test_09092019GBL",
    "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
    "targetPartnerName": "Test_Test_09032019GBL",
    "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "lastModifiedUser": "edc0524d-2e42-4619-af7e-349c015cfdfd",
    "lineItems": [
      {
        "id": 0,
        "subscriptionId": "586DFB1A-E65C-48F4-BF6C-0D62D68AF1D0",
        "offerId": "B4D4B7F4-4089-43B6-9C44-DE97B760FB11",
        "billingCycle": "monthly",
        "friendlyName": "Visio Online Plan 2",
        "quantity": 1,
        "partnerIdOnRecord": "5139005",
        "addonItems": [

        ]
      },
      {
        "id": 0,
        "subscriptionId": "1151B8CE-125C-49D7-8C48-E62FC9101B77",
        "offerId": "13D32E13-A1B0-400D-96C0-4EAAA14DCED5",
        "billingCycle": "monthly",
        "friendlyName": "Dynamics 365 for Supply Chain Management Attach to Qualifying Dynamics 365 Base Offer (Qualified Offer)",
        "quantity": 20,
        "partnerIdOnRecord": "5139005",
        "addonItems": [

        ]
      }
    ],
    "links": {
      "self": {
        "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ab724652-3442-4912-8615-61525bb9903d",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "objectType": "TransferEntity"
    }
  },
  {
    "id": "38a00d97-421c-4c33-8ae4-c8750604e02c",
    "status": "Complete",
    "createdTime": "2020-02-20T21:16:30.0149083Z",
    "lastModifiedTime": "2020-02-27T01:11:33Z",
    "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
    "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "sourcePartnerName": "Test_Test_09092019GBL",
    "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
    "targetPartnerName": "Test_Test_09032019GBL",
    "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "lastModifiedUser": "edc0524d-2e42-4619-af7e-349c015cfdfd",
    "lineItems": [
      {
        "id": 0,
        "subscriptionId": "25339C80-8C79-49A8-8C38-C98A80F4D3A5",
        "offerId": "5E1087B6-246B-4503-B88A-B60BDF0B3840",
        "orderId": "5761e79a-f441-4a18-9902-83f9582ccff6",
        "billingCycle": "monthly",
        "friendlyName": "PowerApps per app plan",
        "quantity": 1,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "0",
        "status": "Complete",
        "addonItems": [

        ]
      },
      {
        "id": 0,
        "subscriptionId": "FE2EA4C8-88EA-41DC-BC2F-76195E282202",
        "offerId": "91FD106F-4B2C-4938-95AC-F54F74E9A239",
        "orderId": "9a088a06-dfe5-4f71-ba79-2711c313b634",
        "billingCycle": "monthly",
        "friendlyName": "Office 365 E1",
        "quantity": 1,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "1",
        "status": "Complete",
        "addonItems": [

        ]
      },
      {
        "id": 0,
        "subscriptionId": "D6C8BF37-CE99-46E1-A64F-329F1971F54D",
        "offerId": "MS-AZR-0145P",
        "orderId": "6a9a544c-54c9-43e9-a863-b40c6f92d111",
        "billingCycle": "monthly",
        "friendlyName": "Microsoft Azure",
        "quantity": 1,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "2",
        "status": "Complete",
        "addonItems": [

        ]
      }
    ],
    "links": {
      "self": {
        "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/38a00d97-421c-4c33-8ae4-c8750604e02c",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "objectType": "TransferEntity"
    }
  },
  {
    "id": "d4f478d2-61e0-4550-b85d-c427abfe1e62",
    "status": "Complete",
    "createdTime": "2020-02-20T21:28:55.4245587Z",
    "lastModifiedTime": "2020-02-20T21:29:22Z",
    "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
    "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "sourcePartnerName": "Test_Test_09092019GBL",
    "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
    "targetPartnerName": "Test_Test_09032019GBL",
    "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "lastModifiedUser": "edc0524d-2e42-4619-af7e-349c015cfdfd",
    "lineItems": [
      {
        "id": 0,
        "subscriptionId": "586DFB1A-E65C-48F4-BF6C-0D62D68AF1D0",
        "offerId": "B4D4B7F4-4089-43B6-9C44-DE97B760FB11",
        "orderId": "2340952e-af72-40e6-a106-e9b2aca99bb5",
        "billingCycle": "monthly",
        "friendlyName": "Visio Online Plan 2",
        "quantity": 2,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "0",
        "status": "Complete",
        "addonItems": [

        ]
      },
      {
        "id": 0,
        "subscriptionId": "6D63E69C-7551-4E37-B7F6-87AC124B3235",
        "offerId": "F1A2FDB0-5CA8-475D-8CCC-9BB81C033DA5",
        "orderId": "5dd120ab-10a4-4bbf-b2bd-e52657431f85",
        "billingCycle": "monthly",
        "friendlyName": "Dynamics 365 for Project Service Automation (Qualified Offer) (250 seat minimum requirement)",
        "quantity": 250,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "1",
        "status": "Complete",
        "addonItems": [

        ]
      }
    ],
    "links": {
      "self": {
        "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/d4f478d2-61e0-4550-b85d-c427abfe1e62",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "objectType": "TransferEntity"
    }
  },
  {
    "id": "f10421cd-d4af-4939-82b9-cd0e75022759",
    "status": "PartiallyComplete",
    "createdTime": "2020-02-26T21:54:51.2901506Z",
    "lastModifiedTime": "2020-02-27T01:10:26Z",
    "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
    "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "sourcePartnerName": "Test_Test_09092019GBL",
    "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
    "targetPartnerName": "Test_Test_09032019GBL",
    "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "lastModifiedUser": "edc0524d-2e42-4619-af7e-349c015cfdfd",
    "lineItems": [
      {
        "id": 0,
        "subscriptionId": "586DFB1A-E65C-48F4-BF6C-0D62D68AF1D0",
        "offerId": "B4D4B7F4-4089-43B6-9C44-DE97B760FB11",
        "billingCycle": "monthly",
        "friendlyName": "Visio Online Plan 2",
        "quantity": 2,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "0",
        "status": "Failed",
        "addonItems": [

        ],
        "transferError": "Subscription has already been transfered. Subscription: 586dfb1a-e65c-48f4-bf6c-0d62d68af1d0"
      },
      {
        "id": 0,
        "subscriptionId": "E9C06692-4D85-411E-8C4A-45E3D6D24EDD",
        "offerId": "1B4642E5-C69A-43EA-B4F6-F29BAE46227E",
        "orderId": "0e6793f0-3d9c-4749-b50d-1cf3527aa454",
        "billingCycle": "monthly",
        "friendlyName": "Dynamics 365 for Retail Attach to Qualifying Dynamics 365 Base Offer From SA From VL/DPL",
        "quantity": 20,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "1",
        "status": "Complete",
        "addonItems": [

        ]
      }
    ],
    "links": {
      "self": {
        "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/f10421cd-d4af-4939-82b9-cd0e75022759",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "objectType": "TransferEntity"
    }
  },
  {
    "id": "ddb933ad-02f4-4678-a09a-7fecca481acc",
    "status": "Reject",
    "createdTime": "2020-03-11T17:44:26.8841412Z",
    "lastModifiedTime": "2020-03-11T17:45:08Z",
    "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
    "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "sourcePartnerName": "Test_Test_09092019GBL",
    "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
    "targetPartnerName": "Test_Test_09032019GBL",
    "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "lastModifiedUser": "01a7548d-1136-4cf0-ba9a-300f921ffb22",
    "lineItems": [
      {
        "id": 0,
        "subscriptionId": "68ECA8B4-A5E7-4245-94FB-A7A81F3B7234",
        "offerId": "5B04B78C-FD36-4CF3-A7A5-3457991C8B79",
        "billingCycle": "monthly",
        "friendlyName": "Dynamics 365 Business Central Device",
        "quantity": 1,
        "partnerIdOnRecord": "5139005",
        "addonItems": [

        ]
      },
      {
        "id": 1,
        "subscriptionId": "F09A8540-AE89-4B08-8967-1ECB92FEE35B",
        "offerId": "MS-AZR-0145P",
        "billingCycle": "monthly",
        "friendlyName": "Microsoft Azure",
        "quantity": 1,
        "partnerIdOnRecord": "5139005",
        "addonItems": [

        ]
      }
    ],
    "links": {
      "self": {
        "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ddb933ad-02f4-4678-a09a-7fecca481acc",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "objectType": "TransferEntity"
    }
  },
  {
    "id": "0a25bd0e-e6c1-40ac-9e96-40b56d46e902",
    "status": "Complete",
    "createdTime": "2020-03-11T17:56:53.622599Z",
    "lastModifiedTime": "2020-03-11T17:58:00Z",
    "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
    "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "sourcePartnerName": "Test_Test_09092019GBL",
    "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
    "targetPartnerName": "Test_Test_09032019GBL",
    "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "lastModifiedUser": "edc0524d-2e42-4619-af7e-349c015cfdfd",
    "lineItems": [
      {
        "id": 0,
        "subscriptionId": "68ECA8B4-A5E7-4245-94FB-A7A81F3B7234",
        "offerId": "5B04B78C-FD36-4CF3-A7A5-3457991C8B79",
        "orderId": "42436b2f-d417-4642-bb76-feb697184100",
        "billingCycle": "monthly",
        "friendlyName": "Dynamics 365 Business Central Device",
        "quantity": 1,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "0",
        "status": "Complete",
        "addonItems": [

        ]
      },
      {
        "id": 1,
        "subscriptionId": "F09A8540-AE89-4B08-8967-1ECB92FEE35B",
        "offerId": "MS-AZR-0145P",
        "orderId": "d9a1b396-ad2c-4283-a9fe-5490acd0ce7d",
        "billingCycle": "monthly",
        "friendlyName": "Microsoft Azure",
        "quantity": 1,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "1",
        "status": "Complete",
        "addonItems": [

        ]
      }
    ],
    "links": {
      "self": {
        "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/0a25bd0e-e6c1-40ac-9e96-40b56d46e902",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "objectType": "TransferEntity"
    }
  },
  {
    "id": "8dc673dd-d6a6-4739-9e8f-0b66bbf2a2c8",
    "status": "Complete",
    "createdTime": "2020-03-19T23:21:03.2754503Z",
    "lastModifiedTime": "2020-03-19T23:22:33Z",
    "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
    "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "sourcePartnerName": "Test_Test_09092019GBL",
    "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
    "targetPartnerName": "Test_Test_09032019GBL",
    "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "lastModifiedUser": "3badf44d-fd41-4432-a17d-214e31f2d9ee",
    "lineItems": [
      {
        "id": 0,
        "subscriptionId": "F5B2EB56-9E0E-4160-9CEE-4218D1EEADDB",
        "offerId": "3DD9350B-27D6-4501-93A4-C8D107F1DE47",
        "orderId": "31bfde4a-efca-49b2-b210-62973fb773db",
        "billingCycle": "monthly",
        "friendlyName": "Microsoft Flow Plan 1 (Qualified Offer)",
        "quantity": 1,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "0",
        "status": "Complete",
        "addonItems": [

        ]
      }
    ],
    "links": {
      "self": {
        "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/8dc673dd-d6a6-4739-9e8f-0b66bbf2a2c8",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "objectType": "TransferEntity"
    }
  },
  {
    "id": "ac4a9d22-ba07-444e-890f-cfe084eed498",
    "status": "Reject",
    "createdTime": "2020-03-25T22:05:25.1057725Z",
    "lastModifiedTime": "2020-03-27T17:50:32Z",
    "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
    "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "sourcePartnerName": "Test_Test_09092019GBL",
    "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
    "targetPartnerName": "Test_Test_09032019GBL",
    "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "lastModifiedUser": "01a7548d-1136-4cf0-ba9a-300f921ffb22",
    "lineItems": [
      {
        "id": 0,
        "subscriptionId": "1151B8CE-125C-49D7-8C48-E62FC9101B77",
        "offerId": "13D32E13-A1B0-400D-96C0-4EAAA14DCED5",
        "billingCycle": "monthly",
        "friendlyName": "Dynamics 365 for Supply Chain Management Attach to Qualifying Dynamics 365 Base Offer (Qualified Offer)",
        "quantity": 20,
        "partnerIdOnRecord": "5139005",
        "addonItems": [

        ]
      }
    ],
    "links": {
      "self": {
        "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "objectType": "TransferEntity"
    }
  },
  {
    "id": "7b1ce5e6-5829-45c6-b3bb-89bfb791a69e",
    "status": "PartiallyComplete",
    "createdTime": "2020-03-25T22:20:38.8090876Z",
    "lastModifiedTime": "2020-03-25T22:24:35Z",
    "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
    "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "sourcePartnerName": "Test_Test_09092019GBL",
    "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
    "targetPartnerName": "Test_Test_09032019GBL",
    "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
    "lastModifiedUser": "edc0524d-2e42-4619-af7e-349c015cfdfd",
    "lineItems": [
      {
        "id": 0,
        "subscriptionId": "2FAFDD44-1891-4EEA-9928-A07B558825C5",
        "offerId": "5344C201-3099-44E5-B333-C3EB0401EDE0",
        "orderId": "21b92393-ffce-4bc7-87c5-62cfa897d8f9",
        "billingCycle": "annual",
        "friendlyName": "Dynamics 365 Customer Engagement Plan (36 mo)",
        "quantity": 1,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "0",
        "status": "Complete",
        "addonItems": [

        ]
      },
      {
        "id": 1,
        "subscriptionId": "637FF8F6-D842-4573-8DA8-89765356CD1A",
        "offerId": "A4179D30-CC09-49F0-977E-DC2CB70B874F",
        "billingCycle": "annual",
        "friendlyName": "Project Online Essentials",
        "quantity": 1,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "1",
        "status": "Failed",
        "addonItems": [

        ],
        "transferError": "Subscription SyncState must be SyncComplete for the Subscription to be a source in a Subscription Ownership Transfer. Subscription: 637ff8f6-d842-4573-8da8-89765356cd1a, current state: None"
      },
      {
        "id": 2,
        "subscriptionId": "41D4FD77-1EB3-425A-BF40-88B8461D39B2",
        "offerId": "1A90EE13-2CB4-4785-BB0F-542813F00A37",
        "orderId": "7414b8ea-c167-4cc4-bc8e-b43efc177a46",
        "billingCycle": "annual",
        "friendlyName": "Dynamics 365 Business Central Essential",
        "quantity": 1,
        "partnerIdOnRecord": "5139005",
        "transferGroupId": "2",
        "status": "Complete",
        "addonItems": [

        ]
      }
    ],
    "links": {
      "self": {
        "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/7b1ce5e6-5829-45c6-b3bb-89bfb791a69e",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "objectType": "TransferEntity"
    }
  }
]
```
